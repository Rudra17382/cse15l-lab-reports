# CSE 15L Fall 2022 Lab Report 2


Hello and welcome to lab reports for CSE 15L. This week we will learn how to write a simple search engine and fixing bugs in code examples

## Part 1: Simple Search Engine from Week 2

### SearchEngine.java
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

/**
 * Boiler Plate Code copied from NumberServer.java
 */

 
/**
 * Handler that handles requests, interacts with the storage
 * accesses it and manipulate it.
 */
class Handler implements URLHandler {

    //Identifier for invalid query. DO NOT SHARE. Update if leaked.
    String invalidQueryIndentifier = "5d6870408eba79cbf114";

    /**
     * Storage of the list of strings that will be accessed 
     * and manipulated by the user
     */
    ArrayList<String> listOfStrings = new ArrayList<String>();

    /**
     * Split the query in the argument url.
     * Use = as the split operator to split around
     * @param url URL to split the query of
     * @return string list of split query around =
     */
    public String[] splitQuery(URI url) {
        return url.getQuery().split("=");
    }

    /**
     * Validate the given query by checking that format "s=abc" is 
     * being followed in the query
     * @param url Input URL
     * @return validated query string or invalid identifier
     */
    public String validateQuery(URI url) {

        //Splitting the query
        String[] query = splitQuery(url);

        //Check if first element is "s" otherwise return invalid query
        if (query[0].equals("s")) {
            return query[1];
        } 
        return invalidQueryIndentifier;
    }

    /**
     * The deafult path that webpage goes back to
     * @return webpage with the current list of strings
     */
    public String defaultPath() {
        return "Current list: " + String.join(", ", listOfStrings);
    }
    
    /**
     * Search function to search and find out if the given 
     * query is in one or more of the strings in the list of strings
     * @param url Input URL
     * @return Webpage with a list of strings that contain the query
     */
    public String search(URI url) {

        // Validate the query; make an arraylist to store correct strings
        String query = validateQuery(url);
        ArrayList<String> matchingResults = new ArrayList<String>();

        // Invalid query
        if (query.equals(invalidQueryIndentifier)) {
            return "Invalid Path and/or Query";
        }

        // Checking for every string in list of strings
        for (String string : listOfStrings) {
            //Add to matchingResults arraylist if string contains query
            if (string.contains(query)) {
                matchingResults.add(string);
            }
        }

        // If there is atleast one result then return the webpage
        if (matchingResults.size() > 0) {
            return (
                "Following strings contain the query: " + 
                String.join(", ", matchingResults)
            );
        }

        // No matching strings
        return "No Strings contained the given query :/";
    }

    /**
     * Add function to add the given query to the list of strings
     * @param url Input URL
     * @return Confirmation + Current list
     */
    public String add(URI url) {

        // Validate the query
        String query = validateQuery(url);

        // Invalid Query
        if (query.equals(invalidQueryIndentifier)) {
            return "Invalid Path and/or Query!";
        }

        // Add the query to the list of strings and return confirmation
        listOfStrings.add(query);
        return "Query Added! " + defaultPath();
    }

    /**
     * Handle the given requests in the form of URLs
     * @param url given request in the form of a url
     * @return The resulting webpage to be shown
     */
    public String handleRequest(URI url) {
        // Get the path
        String path = url.getPath();

        // Call function based on given path
        if (path.equals("/")) {
            return defaultPath();
        } else if (path.contains("/search")) {
            return search(url);
        } else if (path.contains("/add")) {
            return add(url);
        } else {
            return "404 Not Found; Invalid Path!";
        }
    }
}


/**
 * Contains the Main method
 */
public class SearchEngine {

    /**
     * Main method
     * Enter port number in command line argument to run
     * a local server on the designated port
     * Visit http://localhost:<port number> to see the server
     * @param args port number is 0th arg
     * @throws IOException
     */
    public static void main(String[] args) throws IOException {

        //Check if port number is specified
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        //parse into string and start a server on the port
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```

### Server.java (Note: Not my code, this is the code given in week 2 lab)
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```


### The code in action:

![default](../Pictures/lab-report-week-3/defaultPath.jpg)

This is the default path. Upon calling this path, Handler.defaultPath() is called which just returns the current list of strings

#### Lets try adding some alt rock artist names and creating a list off that!

![add1](../Pictures/lab-report-week-3/add1.jpg)

This is the add path. It uses the syntax /add?s=thingToAdd. Upon using this path, Handler.handleRequest() calls Handler.add() and passes in the url as one of the arguments. The add method uses the validate method to validate the query which uses the split method to split the query and make sure that its in form s=abc. If the query is invalid then the appropriate message is displayed. If its valid then ArrayList.add() method is called on listOfStrings to add the query in this case David Bowie to the list of Strings. After which a confirmation message is displayed.

![add2](../Pictures/lab-report-week-3/add2.jpg)

What happened in the previous picture but with Thom Yorke in this case.

![add3](../Pictures/lab-report-week-3/add3.jpg)

What happened in the previous two pictures but with multiple other artist names in this case.

![default2](../Pictures/lab-report-week-3/default2.jpg)

Default Path after all the names have been added.

#### Now lets try using the search function to search some names

![search1](../Pictures/lab-report-week-3/search1.jpg) 

This is the search path. It uses the syntax search?s=thingToSearch. Upon using this path, Handler.handleRequest calls Handler.search() passes in the url as one of the arguments. The add method uses the validate method to validate the query which uses the split method to split the query and make sure that its in form s=abc. If the query is invalid then the appropriate message is displayed. If its valid then it searches if any of the strings in the listOfStrings contains the query through a for each loop on the array list. It adds all the elements that contain the query to a seperate list and then show the list. In this case it is using David (First Name) as the query to search for.

![search2](../Pictures/lab-report-week-3/search2.jpg) 

What happened in the previous picture but with Yorke (Last Name) in this case.

![search3](../Pictures/lab-report-week-3/search3.jpg) 

What happened in the previous two pictures but with Lou Reed (Full Name) in this case.

![search4](../Pictures/lab-report-week-3/search4.jpg)

What happened in the previous three pictures but with vi (a common part of multiple names) in this case.

![searchFail2.jpg](../Pictures/lab-report-week-3/searchFail2.jpg)

What happened in the previous four pictures but with a name that does not exist in the list, so it displays the appropriate error message.

#### Now lets try to fail the code and make sure its displaying appropriate messages

![pathFail](../Pictures/lab-report-week-3/pathFail.jpg)

Lets say that I wanted to listen to Thom Yorke of Radiohead now so I put in the above command. It fails and shows the fail message because the path does not exist... yet.

![addFail1](../Pictures/lab-report-week-3/addFail1.jpg)

When you try to add a name but then mistype the s to something else or forget it by mistake.

![searchFail1.jpg](../Pictures/lab-report-week-3/searchFail1.jpg)

When you try to search a name but then mistype the s to something else or forget it by mistake.