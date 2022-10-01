# CSE 15L Fall 2022 Lab Report 1


Hello and welcome to lab reports for CSE 15L. This week we will learn how to remotely connect to a server using ssh and the basic stuff you can do with it. 

## Installing Visual Studio Code
To install visual studio code, follow the given link and the instructions given on the website to install the software onto your personal computer. Visual studio code is a great code editor that will make our lives a lot easier when trying to code.

[Install Visual Studio Code](https://code.visualstudio.com/)

Once you have installed VS Code, it should look something like this.

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/vscode.PNG)

## Remotely Connecting
Now that you have VS Code installed click on terminal at the top of your app and open a new terminal, this is what we will be using to connect to the remote servers.

First, install open ssh using [Install OpenSSH](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui).

Next, type in the following command in your vs code terminal:
`ssh cs15lfa22zz@ieng6.ucsd.edu`

You should get a message like this
```
ssh cs15lfa22zz@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
```
Type in yes to proceed.

```
# Now on remote server
Last login: Sun Jan  2 14:03:05 2022 from 107-217-10-235.lightspeed.sndgca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lfa22zz, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   23:25:01   0  0.08,  0.17,  0.11
ieng6-202   23:25:01   1  0.09,  0.15,  0.11
ieng6-203   23:25:01   1  0.08,  0.15,  0.11

Sun Jan 02, 2022 11:28pm - Prepping cs15lfa22
```

It should look something like this.

Note: The code snippets here are taken from [course website](https://ucsd-cse15l-f22.github.io/week/week1/#week1-lab-report). Pictures of me doing the exact same thing are included below. 

Note: You will probably need to reset your account password to login.

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/first-shh-login.PNG)

## Trying Some Commands

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/trying-out-new-commands.PNG)

Here:  
Ls -lat also tells you when you made the files.
ls is for listing files, mkdir is to make a new directory, cd is to change the current working directory, ~ is the home directory location -lat are modifiers to ls for example -a shows all files, even hidden ones, cp is to copy and cat is to print out the raw text version of the given file.

In the last few commands, first we copy over hello.txt from the public directory under cs15lfa22 to our home directory which is ~. Next, we check the contents of hello.txt in its original location using cat and cross reference it to the copied version of hello.txt in our home directory ~ to make sure it is the same.

## Moving Files with scp

First, let's create a java file that gives us the current system information that it is running on and where it is at in the system (local location)
```
WhereAmI.java
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```

Run the file using 
```
javac WhereAmI.java
java WhereAmI
```

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/local-location.PNG)

Now, lets use scp to copy this file from our local computer to the remote server.

Use the following command
```
scp WhereAmI.java cs15lfa22zz@ieng6.ucsd.edu:~/
```

You will need to enter your ssh password as scp uses ssh and then it should be copied from your local computer to the remote server.

Try running the java file on your local computer and the remote server to see the difference and prove that scp has worked!


![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/scp.PNG)

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/new-whereami.PNG)

## Setting an SSH Key

It can get quite tedious and cumbersome to have to type in the ssh password again and again. Instead you can set up an SSH key to skip this step every single time you login on scp a file onto a remote computer.

Run the command: `ssh-keygen`

It should ask for a prompt on where to save the file, just press enter to save yourself the hassle and note down the file path for later.

It should've created 2 files on your pc, the public and private RSA keys in the .ssh directory. 

Next, lets copy the public key onto the remote server:

```
ssh cs15lfa22zz@ieng6.ucsd.edu
<Enter Password>
mkdir .ssh
exit
```

The above commands should create a hidden .ssh directory on the remote server, now you just copy the public key onto this directory.

Use this command to copy it: `scp /Users/<username>/.ssh/id_rsa.pub cs15lfa22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys`

Once you are done with this, you should be able to ssh and scp without having to enter the password every time.

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/ssh-keygen.PNG)

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/ssh-key-transfer.PNG)

![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/logging-in-without-password.PNG)

## Optimizing Remote Running

To optimze commands you are planning to run on the remote sever, there are a few tricks that you can use.

First, you can write your commands in "" after the ssh command to directly run them on the remote server after you login.

For example: 
`ssh cs15lfa22zz@ieng6.ucsd.edu "ls; cd dir1"`
This will log into your cs15l account using ssh and then list all the files and folders in the home directory after which it will change directory to dir1

Next, you can use semicolons to run multiple commands on the same line.

For example:
`cp WhereAmI.java OtherMain.java; javac OtherMain.java; java WhereAmI`
This will copy WhereAmI.java to OtherMain.java, compile OtherMain.java and then run WhereAmI.class.

Lastly, you can use the up arrow key to go to the previous command that you have used.


![Image](https://Rudra17382.github.io/cse15l-lab-reports/Pictures/lab-report-week-1/multiple-commands-at-once.PNG)