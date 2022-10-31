# CSE 15L Fall 2022 Lab Report 3


Hello and welcome to lab reports for CSE 15L. This week, we will learn some command line options for the command "grep"

## Basics on Grep:
Wikipedia defines grep as a command used to search and return lines of a dataset which matches the given expression. [ref1.](https://en.wikipedia.org/wiki/
Grep)

To use grep more generally for our applications, we can pipe it the dataset using | symbol which takes the output from the left side and feeds it to the right side.

```
ls | grep ".txt"
```
This will print all the .txt files in the current directory

```
find * | grep ".txt"
```
This will print all the .txt files in the current and all nested directories within it

## 1) -i: ignore uppercase vs lowercase
This command line option for grep ignores if the given expression to search for is upper case or lower case.  

### Example a)
```
rudrarupani@Rudras-MacBook-Pro technical % find 911report | grep -i "CHAPTER"
911report/chapter-13.4.txt
911report/chapter-13.5.txt
911report/chapter-13.1.txt
911report/chapter-13.2.txt
911report/chapter-13.3.txt
911report/chapter-3.txt
911report/chapter-2.txt
911report/chapter-1.txt
911report/chapter-5.txt
911report/chapter-6.txt
911report/chapter-7.txt
911report/chapter-9.txt
911report/chapter-8.txt
911report/chapter-12.txt
911report/chapter-10.txt
911report/chapter-11.txt
rudrarupani@Rudras-MacBook-Pro technical % find 911report | grep "CHAPTER"
rudrarupani@Rudras-MacBook-Pro technical % 
```

In this case, as we can see even though we put CHAPTER in captial letters as the search expression, it still returned all the chapters from 911 report because of the -i command line option. Without the option it does not return anything.

### Example b)
```
rudrarupani@Rudras-MacBook-Pro technical % find government/Media | grep -i "legal"  
government/Media/Legal-aid_chief.txt
government/Media/Free_legal_service.txt
government/Media/Legal_system_fails_poor.txt
government/Media/Supporting_Legal_Center.txt
government/Media/Providing_Legal_Aid.txt
government/Media/Legal_Aid_in_Clay_County.txt
government/Media/Legal_hotline.txt
government/Media/Poor_Lacking_Legal_Aid.txt
government/Media/Paralegal_Honored.txt
government/Media/Coup_Reshapes_Legal_Aid.txt
government/Media/Legal_Aid_looks_to_legislators.txt
government/Media/Boone_legal_service.txt
government/Media/Free_Legal_Assistance.txt
government/Media/Marylands_Legal_Aid.txt
government/Media/Legal_Aid_Society.txt
government/Media/Valley_Needing_Legal_Services.txt
government/Media/Legal_Aid_attorney.txt
government/Media/Legal_services_for_poor.txt
government/Media/less_legal_aid.txt
government/Media/5_Legal_Groups.txt
government/Media/NJ_Legal_Services.txt
government/Media/Bridging_legal_aid_gap.txt
government/Media/Legal_Aid_campaign.txt
rudrarupani@Rudras-MacBook-Pro technical % find government/Media | grep "legal"   
government/Media/Free_legal_service.txt
government/Media/Paralegal_Honored.txt
government/Media/Boone_legal_service.txt
government/Media/less_legal_aid.txt
government/Media/Bridging_legal_aid_gap.txt
rudrarupani@Rudras-MacBook-Pro technical % 
```

This example better demonstrates the usefulness of -i command line option. In this case, we have many files on legal matter but with inconsistent naming in terms of upper case and lower case. In this case, you need to use the -i modifier to return all files with legal in their name, otherwise you may miss out on different casing on letters due to human error or someone just not being good at naming files consistently.

### Example c)
```
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i "gb"
biomed/gb-2002-4-1-r2.txt
biomed/gb-2003-4-6-r41.txt
biomed/gb-2001-2-4-research0010.txt
biomed/gb-2003-4-4-r24.txt
biomed/gb-2001-2-4-research0011.txt
biomed/gb-2003-4-5-r34.txt
biomed/gb-2002-4-1-r1.txt
biomed/gb-2002-3-9-research0043.txt
biomed/gb-2001-2-7-research0025.txt
biomed/gb-2002-3-7-research0032.txt
biomed/gb-2003-4-4-r26.txt
biomed/gb-2001-2-4-research0012.txt
biomed/gb-2001-2-7-research0024.txt
biomed/gb-2001-2-3-research0008.txt
biomed/gb-2003-4-7-r46.txt
biomed/gb-2003-4-7-r42.txt
biomed/gb-2002-3-9-research0046.txt
biomed/gb-2002-3-7-research0037.txt
biomed/gb-2001-2-8-research0027.txt
biomed/gb-2001-2-11-research0046.txt
biomed/gb-2001-2-8-research0032.txt
biomed/gb-2002-3-7-research0036.txt
biomed/gb-2003-4-5-r32.txt
biomed/gb-2003-4-7-r43.txt
biomed/gb-2003-4-5-r30.txt
biomed/gb-2002-3-9-research0051.txt
biomed/gb-2002-3-9-research0045.txt
biomed/gb-2001-2-8-research0030.txt
biomed/gb-2001-2-4-research0014.txt
biomed/gb-2001-2-11-research0045.txt
biomed/gb-2002-3-7-research0035.txt
biomed/gb-2001-2-8-research0031.txt
biomed/gb-2002-3-9-research0044.txt
biomed/gb-2002-3-2-research0008.txt
biomed/gb-2002-3-11-research0059.txt
biomed/gb-2002-3-11-research0065.txt
biomed/gb-2003-4-9-r58.txt
biomed/gb-2003-4-2-r16.txt
biomed/gb-2001-2-10-research0041.txt
biomed/gb-2002-3-8-research0040.txt
biomed/gb-2001-2-9-research0035.txt
biomed/gb-2003-4-6-r37.txt
biomed/gb-2002-3-12-research0085.txt
biomed/gb-2002-3-2-research0009.txt
biomed/gb-2002-3-6-software0001.txt
biomed/gb-2002-3-12-research0087.txt
biomed/gb-2002-3-12-research0078.txt
biomed/gb-2001-2-6-research0018.txt
biomed/gb-2001-2-9-research0037.txt
biomed/gb-2003-4-2-r14.txt
biomed/gb-2001-2-10-research0042.txt
biomed/gb-2002-3-12-research0079.txt
biomed/gb-2002-3-12-research0086.txt
biomed/gb-2002-3-12-research0082.txt
biomed/gb-2001-2-6-research0021.txt
biomed/gb-2003-4-2-r11.txt
biomed/gb-2001-2-6-research0020.txt
biomed/gb-2002-3-12-research0083.txt
biomed/gb-2002-3-11-research0062.txt
biomed/gb-2002-3-11-research0060.txt
biomed/gb-2002-3-12-research0081.txt
biomed/gb-2003-4-9-r60.txt
biomed/gb-2003-4-3-r17.txt
biomed/gb-2002-3-12-research0080.txt
biomed/gb-2002-3-11-research0061.txt
biomed/gb-2002-3-12-research0072.txt
biomed/gb-2003-4-1-r5.txt
biomed/gb-2002-3-12-research0071.txt
biomed/gb-2000-1-1-research002.txt
biomed/gb-2001-3-1-research0005.txt
biomed/gb-2003-4-1-r7.txt
biomed/gb-2002-3-5-research0024.txt
biomed/gb-2002-3-5-research0025.txt
biomed/gb-2001-3-1-research0004.txt
biomed/gb-2003-4-3-r18.txt
biomed/gb-2001-2-2-research0004.txt
biomed/gb-2003-4-6-r39.txt
biomed/gb-2003-4-3-r20.txt
biomed/gb-2003-4-9-r57.txt
biomed/gb-2002-3-5-research0021.txt
biomed/gb-2002-3-5-research0020.txt
biomed/gb-2001-3-1-research0001.txt
biomed/gb-2002-3-12-research0075.txt
biomed/gb-2002-3-12-research0088.txt
biomed/gb-2002-3-12-research0077.txt
biomed/gb-2003-4-8-r51.txt
biomed/gb-2002-3-5-research0022.txt
biomed/gb-2002-3-5-research0023.txt
biomed/gb-2002-3-6-research0029.txt
biomed/gb-2003-4-8-r50.txt
biomed/gb-2002-3-9-research0049.txt
biomed/gb-2002-3-9-research0048.txt
biomed/gb-2002-3-10-research0052.txt
biomed/gb-2003-4-2-r9.txt
biomed/gb-2001-2-12-research0055.txt
biomed/gb-2002-3-4-research0019.txt
biomed/gb-2002-3-4-research0018.txt
biomed/gb-2001-2-12-research0054.txt
biomed/gb-2003-4-2-r8.txt
biomed/gb-2002-3-10-research0053.txt
biomed/gb-2002-3-3-research0012.txt
biomed/gb-2000-1-2-research0003.txt
biomed/gb-2002-3-8-research0039.txt
biomed/gb-2001-2-12-research0051.txt
biomed/gb-2002-3-8-research0038.txt
biomed/gb-2002-3-10-research0056.txt
biomed/gb-2002-3-3-research0011.txt
biomed/gb-2002-3-10-research0054.txt
biomed/gb-2001-2-12-research0053.txt
biomed/gb-2003-4-4-r28.txt
biomed/gb-2001-2-3-research0007.txt
biomed/gb-2002-3-10-research0055.txt
rudrarupani@Rudras-MacBook-Pro technical % 
```

In this case, it was not entirely necessary to use -i command line option because all of the search expression is already in small in all files. Sometimes it is still better to be safe than sorry and include -i.

## 2) -v invert match
This command line for grep returns all the lines that do NOT match with the given expression. 

### Example a)
```
rudrarupani@Rudras-MacBook-Pro technical % find plos | grep -v -i "journal"
plos
plos/pmed.0020273.txt
plos/pmed.0020065.txt
plos/pmed.0020071.txt
plos/pmed.0020059.txt
plos/pmed.0010039.txt
plos/pmed.0010010.txt
plos/pmed.0020104.txt
plos/pmed.0020272.txt
plos/pmed.0020258.txt
plos/pmed.0020099.txt
plos/pmed.0010013.txt
plos/pmed.0020113.txt
plos/pmed.0020098.txt
plos/pmed.0020067.txt
plos/pmed.0020073.txt
plos/pmed.0020249.txt
plos/pmed.0020275.txt
plos/pmed.0020088.txt
plos/pmed.0020103.txt
plos/pmed.0020117.txt
plos/pmed.0020116.txt
plos/pmed.0020102.txt
plos/pmed.0020062.txt
plos/pmed.0020274.txt
plos/pmed.0020048.txt
plos/pmed.0020060.txt
plos/pmed.0020074.txt
plos/pmed.0020114.txt
plos/pmed.0010028.txt
plos/pmed.0010029.txt
plos/pmed.0020115.txt
plos/pmed.0020075.txt
plos/pmed.0020061.txt
plos/pmed.0020210.txt
plos/pmed.0020238.txt
plos/pmed.0010066.txt
plos/pmed.0020198.txt
plos/pmed.0010067.txt
plos/pmed.0020007.txt
plos/pmed.0020239.txt
plos/pmed.0020005.txt
plos/pmed.0020039.txt
plos/pmed.0010071.txt
plos/pmed.0010058.txt
plos/pmed.0010070.txt
plos/pmed.0010064.txt
plos/pmed.0020158.txt
plos/pmed.0020206.txt
plos/pmed.0020212.txt
plos/pmed.0020216.txt
plos/pmed.0020028.txt
plos/pmed.0020148.txt
plos/pmed.0020160.txt
plos/pmed.0010048.txt
plos/pmed.0010060.txt
plos/pmed.0010061.txt
plos/pmed.0010049.txt
plos/pmed.0020161.txt
plos/pmed.0020149.txt
plos/pmed.0020015.txt
plos/pmed.0020203.txt
plos/pmed.0020201.txt
plos/pmed.0020017.txt
plos/pmed.0010062.txt
plos/pmed.0020189.txt
plos/pmed.0020162.txt
plos/pmed.0020016.txt
plos/pmed.0020002.txt
plos/pmed.0020200.txt
plos/pmed.0020231.txt
plos/pmed.0020027.txt
plos/pmed.0020033.txt
plos/pmed.0010047.txt
plos/pmed.0010046.txt
plos/pmed.0010052.txt
plos/pmed.0020191.txt
plos/pmed.0020146.txt
plos/pmed.0020232.txt
plos/pmed.0020226.txt
plos/pmed.0020024.txt
plos/pmed.0020018.txt
plos/pmed.0020144.txt
plos/pmed.0020150.txt
plos/pmed.0020187.txt
plos/pmed.0010050.txt
plos/pmed.0010051.txt
plos/pmed.0020192.txt
plos/pmed.0010045.txt
plos/pmed.0020145.txt
plos/pmed.0020019.txt
plos/pmed.0020237.txt
plos/pmed.0020009.txt
plos/pmed.0020035.txt
plos/pmed.0020021.txt
plos/pmed.0020155.txt
plos/pmed.0010069.txt
plos/pmed.0010041.txt
plos/pmed.0020182.txt
plos/pmed.0020196.txt
plos/pmed.0020197.txt
plos/pmed.0010068.txt
plos/pmed.0020140.txt
plos/pmed.0020020.txt
plos/pmed.0020034.txt
plos/pmed.0020236.txt
plos/pmed.0020208.txt
plos/pmed.0020022.txt
plos/pmed.0020036.txt
plos/pmed.0010056.txt
plos/pmed.0020195.txt
plos/pmed.0010042.txt
plos/pmed.0020181.txt
plos/pmed.0020180.txt
plos/pmed.0020194.txt
plos/pmed.0020157.txt
plos/pmed.0020023.txt
plos/pmed.0020235.txt
plos/pmed.0020209.txt
plos/pmed.0020246.txt
plos/pmed.0020050.txt
plos/pmed.0020118.txt
plos/pmed.0010030.txt
plos/pmed.0010024.txt
plos/pmed.0010025.txt
plos/pmed.0020086.txt
plos/pmed.0020045.txt
plos/pmed.0020247.txt
plos/pmed.0020047.txt
plos/pmed.0020090.txt
plos/pmed.0010026.txt
plos/pmed.0020085.txt
plos/pmed.0020091.txt
plos/pmed.0020278.txt
plos/pmed.0020268.txt
plos/pmed.0010022.txt
plos/pmed.0010036.txt
plos/pmed.0010023.txt
plos/pmed.0020123.txt
plos/pmed.0020094.txt
plos/pmed.0020257.txt
plos/pmed.0020055.txt
plos/pmed.0020082.txt
plos/pmed.0010021.txt
plos/pmed.0010034.txt
plos/pmed.0010008.txt
plos/pmed.0020120.txt
plos/pmed.0020040.txt
plos/pmed.0020068.txt
plos/pmed.0020281.txt
plos/pmed.0020242.txt
rudrarupani@Rudras-MacBook-Pro technical % 
```

Lets say we wanted to skip all the journal entries then this command could be very useful.

### Example b)
```
rudrarupani@Rudras-MacBook-Pro technical % find plos | grep -i "journal" | grep -v -i "0020"
plos/journal.pbio.0030032.txt
plos/journal.pbio.0030024.txt
plos/journal.pbio.0030021.txt
plos/journal.pbio.0030051.txt
plos/journal.pbio.0030131.txt
plos/journal.pbio.0030050.txt
plos/journal.pbio.0030127.txt
plos/journal.pbio.0030094.txt
plos/journal.pbio.0030137.txt
plos/journal.pbio.0030136.txt
plos/journal.pbio.0030056.txt
plos/journal.pbio.0030097.txt
plos/journal.pbio.0030105.txt
plos/journal.pbio.0030065.txt
plos/journal.pbio.0030076.txt
plos/journal.pbio.0030062.txt
plos/journal.pbio.0030102.txt
plos/journal.pbio.0030129.txt
rudrarupani@Rudras-MacBook-Pro technical % 
```

Lets say that we wanted all the journal entires excluding the 20000 series, then we can chain grep two times using pipe to achieve the result. The first grep filters out all the non journal entries and the second one filters out all the 0020 entries. In the end we are left with journal entries that do not start with 0020

### Example c)
```
rudrarupani@Rudras-MacBook-Pro technical % find government/Media | grep -i -v "legal"
government/Media
government/Media/Federal_agency.txt
government/Media/water_fees.txt
government/Media/Helping_Out.txt
government/Media/balance_scales_of_justice.txt
government/Media/BusinessWire2.txt
government/Media/Unusual_Woodburn.txt
government/Media/Funding_cuts_force.txt
government/Media/Good_guys_reward.txt
government/Media/Anthem_Payout.txt
government/Media/Donald_Hilliker.txt
government/Media/Owning_a_Piece.txt
government/Media/Targeting_Domestic_Violence.txt
government/Media/highlight_Senior_Day.txt
government/Media/State_funding.txt
government/Media/Few_who_need.txt
government/Media/City_Council_Budget.txt
government/Media/Lindsays_legacy.txt
government/Media/New_funding_sources.txt
government/Media/Barnes_new_job.txt
government/Media/Nonprofit_Buys.txt
government/Media/Domestic_Violence_Ruling.txt
government/Media/Abuse_penalties.txt
government/Media/Law_Award_from_College.txt
government/Media/Law_Schools.txt
government/Media/Raising_the_Bar.txt
government/Media/Justice_for_all.txt
government/Media/agency_expands.txt
government/Media/Helping_Hands.txt
government/Media/not_accessible_to_disabled.txt
government/Media/Campaign_Pays.txt
government/Media/New_Online_Resources.txt
government/Media/Annual_Fee.txt
government/Media/Oregon_Poor.txt
government/Media/Barnes_pro_bono.txt
government/Media/Workers_aid_center.txt
government/Media/Philly_Lawyers.txt
government/Media/Too_Crucial_to_Take_Cut.txt
government/Media/Pro_Bono_Services.txt
government/Media/Rumble_in_the_Bronx.txt
government/Media/FortWorthStarTelegram.txt
government/Media/predatory_loans.txt
government/Media/Survey.txt
government/Media/AP_LawSchoolDebts.txt
government/Media/Working_for_Free.txt
government/Media/Eviction_law.txt
government/Media/Law-school_grads.txt
government/Media/FY_04_Budget_Outlook.txt
government/Media/help_rent-to-own_tenants.txt
government/Media/Texas_Lawyer.txt
government/Media/Disaster_center.txt
government/Media/Kiosks_for_court_forms.txt
government/Media/Higher_Registration_Fees.txt
government/Media/Fire_Victims_Sue.txt
government/Media/Funds_Shortage.txt
government/Media/Terrorist_Attack.txt
government/Media/Butler_Co_attorneys.txt
government/Media/BergenCountyRecord.txt
government/Media/families_saved.txt
government/Media/Court_Keeps_Judge_From.txt
government/Media/Volunteers_Step_Up.txt
government/Media/IOLTA_INTEREST_RATE.txt
government/Media/Ginny_Kilgore.txt
government/Media/Poverty_Lawyers.txt
government/Media/Wingates_winds.txt
government/Media/Avoids_Budget_Cut.txt
government/Media/grants_fail_to_come.txt
government/Media/Lockyer_Warns.txt
government/Media/It_Pays_to_Know.txt
government/Media/Self-Help_Website.txt
government/Media/Rental_rules.txt
government/Media/Using_Tech_Tools.txt
government/Media/Assuring_Underprivileged.txt
government/Media/Firm_to_the_Poor_Needs_Help.txt
government/Media/Making_a_case.txt
government/Media/Barnes_Volunteers.txt
government/Media/Commercial_Appeal.txt
government/Media/Justice_requests.txt
government/Media/Local_Attorneys.txt
government/Media/Texas_Supreme_Court.txt
government/Media/Civil_Matters.txt
government/Media/Low-income_children.txt
government/Media/man_on_national_team.txt
government/Media/BusinessWire.txt
government/Media/Funding_May_Limit.txt
government/Media/The_Columbian.txt
government/Media/Higher_court.txt
government/Media/Service_Agency.txt
government/Media/Bias_on_the_Job.txt
government/Media/Attorney_gives_his_time.txt
government/Media/Library_Lawyers.txt
government/Media/Crains_New_York_Business.txt
government/Media/Hard_to_Get.txt
government/Media/The_State_of_Pro_Bono.txt
government/Media/residents_sue_city.txt
government/Media/GreensburgDailyNews.txt
government/Media/Major_Changes.txt
government/Media/Program_Lodges.txt
government/Media/Wilmington_lawyer.txt
government/Media/All_May_Have_Justice.txt
government/Media/Domestic_violence_aid.txt
government/Media/Advocate_for_Poor.txt
government/Media/fight_domestic_abuse.txt
government/Media/CommercialAppealMemphis2.txt
government/Media/Weak_economy.txt
government/Media/Lawyer_Web_Survey.txt
government/Media/Barr_sharpening_ax.txt
government/Media/The_Bend_Bulletin.txt
government/Media/Farm_workers.txt
government/Media/Entities_Merge.txt
government/Media/Understanding.txt
government/Media/Do-it-yourself_divorce.txt
government/Media/Politician_Practices.txt
government/Media/defend_yourself.txt
government/Media/Towson_Attorney.txt
government/Media/Pro-bono_road_show.txt
government/Media/A_Perk_of_Age.txt
government/Media/A_helping_hand.txt
government/Media/pro_bono_efforts.txt
government/Media/Greedy_Generous.txt
government/Media/Retirement_Has_Its_Appeal.txt
government/Media/RoanokeTimes.txt
government/Media/Aid_Gets_7_Million.txt
rudrarupani@Rudras-MacBook-Pro technical % 
```

From the example about legal matters in the first command, we can now modify it to exclude all the files that talk about legal matter which may help narrow down the selection of files we need to find.

## 3) -c Output count of matching lines

-c Command line option gives us the line count of all the lines that have the given expression. This can be very useful when you want to find out how many files are there about something. It can also be very useful for statistics and data science.

### Example a)
```
rudrarupani@Rudras-MacBook-Pro technical % find government/Media | grep -i -c "legal"   
23
rudrarupani@Rudras-MacBook-Pro technical % find government/Media | grep -i -v -c "legal"
123
rudrarupani@Rudras-MacBook-Pro technical % find government/Media | grep -i -c ".txt"    
145
```

The first command gives the count of all the files talking about legal matter, the second command gives the count of all the files that are not talking about legal matter + name of the directory, and the last command gives the count of all .txt files in the directory which is all legal files + non legal files - 1 for the count of the directory in non legal files. 23 + 123 - 1 = 145. 

### Example b)
```
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -c "1471"       
444
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -v -c "1471" 
394
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -c "1472" 
99
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -v -c "1472"
739
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -c "1473"   
0
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -v -c "1473"
838
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -c "1474"   
0
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -c "1475"
27
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -v -c "1475"
811
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -c "gb"     
112
rudrarupani@Rudras-MacBook-Pro technical % find biomed | grep -i -v "147" | grep -i -v -c "gb"
105
```

Finding all the files with 1471, 1472, etc. and all the files without them. Finding files with "gb" and then finding files that excluse "147" and "gb" as well. We ca do a lot of creative filtering here

### Example c)
```
rudrarupani@Rudras-MacBook-Pro technical % find plos | grep -i -c "journal"
102
rudrarupani@Rudras-MacBook-Pro technical % find plos | grep -i -v -c "journal"
151
rudrarupani@Rudras-MacBook-Pro technical % find plos | grep -i -c "pmed"       
150
rudrarupani@Rudras-MacBook-Pro technical % find plos | grep -i -v -c "pmed"    
103
```

Finding all the journal entries, non journal entries. Finding all the pmed entries, non pmed entries. Same as before, can be used creatively in many ways.