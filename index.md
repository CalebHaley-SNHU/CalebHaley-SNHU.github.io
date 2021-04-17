# Welcome to Caleb Haley's GitHub Page
On this page, I will be demonstrating some of my skills developed over the course of my at SNHU in three formats: Software Design and Engineering, Algorithms and Data Structure, and Databases.  I will be taking older assignments and enhancing them in some way or another each week.  Ultimately, my goal is for each narrative to work with each other to build a well functioning system.

## Code Review
A YouTube link of my code review is below, the video was far too large for the GitHub limit and it would need to be broken down into 32 different files.                         
[Link to Code Review](https://youtu.be/mReK4KC2xbs)

## Enhancement 1 Narrative: Software Design and Engineering

**A.	Briefly describe the artifact. What is it? When was it created?**

The original program was created in IT-145 and it was a Zoo Monitoring System which was written in Java.  The program would output a menu for the user to select an option on what they wanted to monitor, and the program would read a text file and give the data to the user.  I decided to re-write the program in Python and read JSON files.  I had a JSON file containing some pellet data from work that I repurposed for the program.  This program now outputs a menu for the user to select an option on what they want to monitor, and the program reads a JSON file and gives the data to the user.  The major differences are that rather than spitting out whatever is in the text file, this program finds the data the user is looking for all from within one file.

**B.	Justify the inclusion of the artifact in your ePortfolio. Why did you select this item? What specific components of the artifact showcase your skills and abilities in software development? How was the artifact improved?**

I selected this artifact because I thought it would be a good chance to showcase some of the places I have grown.  I wanted to be able to fine tune what data was coming from the file, something that is commonly done in the field.  We do not always want to retrieve entire files, sometimes we just need bits and pieces.  I enjoy working with data and realize I may be drifting that way professionally, so realistically I want a portfolio that will show my ability to work with data – in other narratives I will be able to work with data a little bit more.  Python is one of the languages used commonly with data analysis so I thought it would be fitting to re-write the application in a language that is naturally well-suited for data analysis. 

**C.	Did you meet the course objectives you planned to meet with this enhancement in Module One? Do you have any updates to your outcome-coverage plans?**

I wanted to achieve CS-409-04 which is to demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals.  I took a program that was able to do the task at hand, but in practice it would be rarely seen; and changed it into a program that written in a language recognized by the industry as one of the most widely used data languages and showcased my ability to pull specific data from a file.

**D.	Reflect on the process of enhancing and/or modifying the artifact. What did you learn as you were creating it and improving it? What challenges did you face?**

The biggest challenge I usually face is biting off more than I can chew.  I always have big, elaborate plans for my programs and at some point, I must realize that I cannot add it all in.  This program was no exception to the rule.  I wanted to add in more data analysis into the program but realized that it was getting overly complex for a user that would just be running a program via command prompt.  Without going back and creating a GUI, some things would just be too hard to do with the user and I found myself losing track of where I was while testing.  I decided to simplify the program to demonstrate the skills that I was aiming for, which I have completed, now I have a working baseline which I can add functions to.  	
This was not something I had done with Python before, I had worked with CSV files in previous courses but had never interacted with a JSON with Python.  This whole program was a learning experience, but it was the learning experience I was aiming for.  I know that Python is used in data science commonly so it would be something that I may need to know in the field.  This program helped engrain some of the practices of using lists and dictionaries in Python for me as well.

### Original Program
``` Java
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.IOException;
public class ZooMonitoringSystem {
    public static void main(String[] args) throws IOException{
      
        Scanner scnr = new Scanner(System.in);

        int userInput = 0;
        Scanner animalDetails = null;
        int detailsInput = 0;
        FileInputStream zooFile = null; 
        String animalLine = "";
        int i = 0;
        Scanner habitatDetails = null;
        String habitatLine = "";
        Scanner animalSubDetails = null;
        Scanner habitatSubDetails = null;
        boolean detailsFound = false;
        
        
        
        while (userInput != 3) {
           
            System.out.println("Do you want to monitor an animal, habitat, or exit?");
            System.out.println("1. Animal ");
            System.out.println("2. Habitat");
            System.out.println("3. Exit");
            System.out.print("Enter your selection: ");
            userInput = scnr.nextInt();
            System.out.println();

            if(userInput == 1){
                zooFile= new FileInputStream("animals.txt");
                animalDetails = new Scanner(zooFile);
                System.out.println("Which animal would you like to monitor?");
                i = 0;
                while (animalDetails.hasNextLine()){
                    animalLine = animalDetails.nextLine(); 
                    if(animalLine.contains("Details")){
                        i++;
                        System.out.println(i + ". " + animalLine);
                    }
                }
                zooFile.close();
                
                System.out.print("Enter your selection: ");
                detailsInput = scnr.nextInt();
                System.out.println();
                zooFile= new FileInputStream("animals.txt");
                animalSubDetails = new Scanner(zooFile);
                i = 0;
                while (animalSubDetails.hasNextLine()){
                    animalLine = animalSubDetails.nextLine(); 
                    if(animalLine.contains("Animal")){
                        i++;
                    }
                    if (i == detailsInput){
                        detailsFound = true;
                        if(animalLine.contains("*****")){
                            String alert = animalLine.substring(5, animalLine.length());
                            int len = alert.length()+12;
                            for (int j = 0; j < len; j++){
                                System.out.print("!");
                            }
                            System.out.println();
                            System.out.println("! WARNING " + alert + " !");
                            for (int j = 0; j < len; j++){
                                System.out.print("!");
                            }
                            System.out.println();
                        }
                        else if(!animalLine.isEmpty()){
                            System.out.println(animalLine);
                        } 
                    }
                    
                }
                if(detailsFound == false){
                    System.out.println("INVALID ENTRY!");
                }                
                zooFile.close();
                System.out.println(); 
            }
            
            else if(userInput == 2){
                zooFile= new FileInputStream("habitats.txt");
                habitatDetails = new Scanner(zooFile);
                System.out.println("Which habitat would you like to monitor?");
                i = 0;
                while (habitatDetails.hasNextLine()){
                    habitatLine = habitatDetails.nextLine(); 
                    if(habitatLine.contains("Details")){
                        i++;
                        System.out.println(i + ". " + habitatLine);
                    }
                    
                }
                zooFile.close();
                System.out.print("Enter your selection: ");
                detailsInput = scnr.nextInt();
                System.out.println();
                zooFile= new FileInputStream("habitats.txt");
                habitatSubDetails = new Scanner(zooFile);
                i = 0;
                while (habitatSubDetails.hasNextLine()){
                    habitatLine = habitatSubDetails.nextLine(); 
                    if(habitatLine.contains("Habitat")){
                        i++;
                    }
                    if (i == detailsInput){
                        detailsFound = true;
                        if(habitatLine.contains("*****")){
                            String alert = habitatLine.substring(5, habitatLine.length());
                            int len = alert.length()+12;
                            for (int j = 0; j < len; j++){
                                System.out.print("!");
                            }
                            System.out.println();
                            System.out.println("! WARNING " + alert + " !");
                            for (int j = 0; j < len; j++){
                                System.out.print("!");
                            }
                            System.out.println();
                        }
                        else if(!habitatLine.isEmpty()){
                            System.out.println(habitatLine);
                        } 
                    }                    
                }
                if(detailsFound == false){
                    System.out.println("INVALID ENTRY!");
                }                  
                zooFile.close();
                System.out.println();
            } 
            else if (userInput == 3){
                break;
            }
            else{
               System.out.println("INVALID ENTRY!");
               System.out.println();
            }
        }
        return;
    }
    
}
```
### Updated Program
``` Python
# Caleb Haley
# CS 499 Capstone
# Southern New Hampshire University
# pelletReader.py

# This program will read data from a JSON file and output the data for the user to see
# The user will be able to select what kind of data they will see from the JSON file using a menu

# import json dependency
import json

# Open the data in file to be read
with open("pellet.json", "r") as string:
    data = json.load(string)
    string.close()


# Defines function to print BTU data
def btu_list(my_dict):
    # Iterate through dictionary if there are still key, value pairs remaining
    for k, v in my_dict.items():
        if isinstance(v, dict):

            print(k + ":")
            btu_list(v)
            continue
        # Finds the brand in JSON file and outputs BTU data
        print("BTU stands for British Temperature Unit - meaning how hot the pellets get")
        print("New England BTU:", str(v[0]['New England'][0]['BTU']))
        print("Okanagan BTU:", str(v[0]['Okanagan'][0]['BTU']))
        print("Maine BTU:", str(v[0]['Maine'][0]['BTU']))
        print("Turman BTU:", str(v[0]['Turman'][0]['BTU']))
        print("Geneva BTU:", str(v[0]['Geneva'][0]['BTU']))
        print("North Idaho BTU:", str(v[0]['North Idaho'][0]['BTU']))
        print("Energex BTU:", str(v[0]['Energex'][0]['BTU']))


# Defines function to print price data
def price_list(my_dict):
    # Iterates as long as key,value pairs are remaining
    for k, v in my_dict.items():
        if isinstance(v, dict):
            print(k + ":")
            price_list(v)
            continue

        print("Price per ton in USD")
        # Finds the brand in JSON and outputs price data
        print("New England price:", str(v[0]['New England'][0]['Price']))
        print("Okanagan price:", str(v[0]['Okanagan'][0]['Price']))
        print("Maine price:", str(v[0]['Maine'][0]['Price']))
        print("Turman price:", str(v[0]['Turman'][0]['Price']))
        print("Geneva price:", str(v[0]['Geneva'][0]['Price']))
        print("North Idaho price:", str(v[0]['North Idaho'][0]['Price']))
        print("Energex price:", str(v[0]['Energex'][0]['Price']))


# Function definition for user menu
def greeting():
    print("Welcome to the Wood Pellet Terminal")
    print("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~")
    print("        Select an option:       ")
    print("1. View Brands")
    print("2. Pellet Pricing in USD")
    print("3. Find Heat content in BTU ")
    print("4. Quit")
    print("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~")


# Bool to easy end program if user chooses
programRunning = True

while programRunning:

    # Calls our greeting function that gives user options
    greeting();
    user_choice = input("Select your option\n")
    i = 0

# Test for user input
    # If user inputs 1, show brands
    if user_choice == "1":
        print("Showing Brands...")
        # Iterates JSON by the first index which is where brand is stored
        brand = [print(i) for i in data['brands'][0]]

    # If user inputs 2, show prices
    elif user_choice == "2":
        print("Printing Price List...")
        # Call the price_list function to print data
        price_list(data)

    # If user inputs 3, show BTU (British Temperature Units)
    elif user_choice == "3":
        print("Printing BTU List...")
        # Call the btu_list function to print data
        btu_list(data)

    # If user chooses 4, the program will stop running
    elif user_choice == "4":
        print("Goodbye")
        # Set our bool to false to close the program
        programRunning = False

    # If the user inputs anything else, it is invalid
    else:
        print("Invalid Input")

```

## Enhancement 2 Narrative: Algorithms and Data Structure

**A.	Briefly describe the artifact. What is it? When was it created?**

The original program was created in IT-145 and it was a system that would ask the user how many apples and oranges they had, and how many they are required to have, then calculate the difference.  I wanted to make the program easier to use for the end-user so I put data into a hash table which contained previous years sales, then the program would ask the user what they would want to calculate and prompt the user for how many of an item they have, then get the last year’s sales data and compare the two numbers.

**B.	Justify the inclusion of the artifact in your ePortfolio. Why did you select this item? What specific components of the artifact showcase your skills and abilities in software development? How was the artifact improved?**

I selected this artifact because the original was extremely simple and clumsy on the user.  I wanted to show how I can accomplish the same task in different ways with varying levels of program depth.  The initial program was a brute force calculating app, and I was able to turn it into something a little more elegant for the user.  This artifact shows my ability to work with different data structures like hash tables and manipulate the data into solving a problem.  This should demonstrate my ability to design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, while managing trade-offs involved in design choices (CS-499-03).

**C.	Did you meet the course objectives you planned to meet with this enhancement in Module One? Do you have any updates to your outcome-coverage plans?**

I wanted to achieve the main course objective mainly, however there was a minor goal I was aiming for in this program that I did fall short on.  Initially, I wanted to re-write the program to read data from a text file, this would be the data containing the previous years’ sales data.  Unfortunately, I was unable to pull that off while still receiving accurate results, for some reason it would keep reading December data every few tests.  Instead, I implemented a hash table which shows my ability to work with different data structures, as I had initially aimed this artifact more towards the algorithm side of the narrative.  

**D.	Reflect on the process of enhancing and/or modifying the artifact. What did you learn as you were creating it and improving it? What challenges did you face?**

In previous courses, I have been introduced to the concepts of certain data structures, but I have never had to implement them on a system of my own or work with them outside of a structured assignment.  I was not familiar with hash tables but after doing research it became clear that using one would be my best chance at this program.  It gave me the ability to cast user input into a variable that I could use to search the dictionary and return the value to the program.  One thing I learned is an appreciation for the Java documentation, I was able to look through documentation at different data structures to find the one that would fit my use in this scenario.  It worked perfectly.  Once I finally broke down and started using the documentation, the program started coming together much better than it was before.  I struggled with this program for a week longer than I initially planned, but I think I was able to take a lot from this narrative.  


### Original Program
``` Java
import java.util.Scanner;

public class StockFruit {
	public static void main(String[] args) {
		// Variable Declarations
		int applesOnHand; // apples currently on hand
		int applesRequired; // apples required to stock
		int orangesOnHand; // oranges currently on hand
		int orangesRequired; // oranges required to stock
		int applesToOrder = 0; // apples to order
		int orangesToOrder = 0; // oranges to order

		Scanner scnr = new Scanner(System.in);

		// input apples on hand
		System.out.println("How many apples are on hand?");
		applesOnHand = scnr.nextInt();

		// input apples that should be in stock
		System.out.println("How many apples should be in stock?");
		applesRequired = scnr.nextInt();

		// input oranges on hand
		System.out.println("How many oranges are on hand?");
		orangesOnHand = scnr.nextInt();

		// input oranges that should be in stock
		System.out.println("How many oranges should be in stock?");
		orangesRequired = scnr.nextInt();

		// determine number of apples needed to order
		if (applesOnHand < applesRequired)
			applesToOrder = applesRequired - applesOnHand;

		// determine number of oranges needed to order
		if (orangesOnHand < orangesRequired)
			orangesToOrder = orangesRequired - orangesOnHand;
		
		// output number of apples that need to be ordered
		if(applesToOrder > 0) {
			System.out.println("Number of apples to order: " + applesToOrder);
		}
		else{
			System.out.println("Number of apples to order: None");
		}
		
		// output number of oranges that need to be ordered
		if(orangesToOrder > 0) {
			System.out.println("Number of oranges to order: " + orangesToOrder);
		}
		else{
			System.out.println("Number of oranges to order: None");
		}
	}
}
```
### Updated Program
``` Java
package StockFruitRevised;

import java.util.Scanner;
import java.util.Dictionary;
import java.util.Enumeration;
import java.util.Hashtable;

public class StockFruitRevised {
	
	// Method definition to print menu of user options
	public static void printMenu() {
		System.out.println("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
		System.out.println("What would you like to do?");
		System.out.println("1. See monthly sales data");
		System.out.println("2. Calculate Apples needed to order");
		System.out.println("3. Calculate Oranges needed to order");
		System.out.println("4. Quit");
		System.out.println("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
	}
	

	// Main function
	public static void main(String[] args) {
		printMenu();
		// Initialize a dictionary to hold apple sales data
				Dictionary<String,Integer> appleSales = new Hashtable<String, Integer>();
				// Input previous sales data into our dictionary
				
				appleSales.put("January", 200);
				appleSales.put("February", 175);
				appleSales.put("March", 150);
				appleSales.put("April", 230);
				appleSales.put("May", 250);
				appleSales.put("June", 300);
				appleSales.put("July", 390);
				appleSales.put("August", 350);
				appleSales.put("September", 200);
				appleSales.put("October", 250);
				appleSales.put("November", 235);
				appleSales.put("December", 190);
				
				// Initialize a dictionary to hold orange sales data
				Dictionary<String,Integer> orangeSales = new Hashtable<>();
				// Input previous sales data into our dictionary
				orangeSales.put("January", 200);
				orangeSales.put("February", 200);
				orangeSales.put("March", 200);
				orangeSales.put("April", 230);
				orangeSales.put("May", 250);
				orangeSales.put("June", 230);
				orangeSales.put("July", 215);
				orangeSales.put("August", 200);
				orangeSales.put("September", 200);
				orangeSales.put("October", 200);
				orangeSales.put("November", 235);
				orangeSales.put("December", 190);
			
		
		// Variable Declarations
		
		boolean programRunning = true;

		Scanner scnr = new Scanner(System.in);
		int userInput = scnr.nextInt(); // Holds user choice
		
		if (programRunning = true) {
			switch(userInput) {
			case 1:
				System.out.println("Entering Sales History...");
				// Ask the user what data they want to see
				System.out.println("Would you like to see Average Apple sales or Average Orange sales?");
				System.out.println("1. Apples");
				System.out.println("2. Oranges");
		
				int userInput1 = scnr.nextInt();
				switch(userInput1) {
				// Case 1 outputs apple sales
				case 1:
					// Enumerate keys and elements
					Enumeration<String> e = appleSales.keys();
					// Keep running if there are more elements
					while(e.hasMoreElements()) {
						String key = e.nextElement();
						// Output key and element
						System.out.println(key + " - " + appleSales.get(key) + " apples");
					}
					break;
				// Case 2 outputs orange sales
				case 2:
					// Enumerate keys and elements
					Enumeration<String> i = orangeSales.keys();
					// Keep running if there are more elements
					while(i.hasMoreElements()) {
						String key = i.nextElement();
						// Output key and element
						System.out.println(key + " - " + orangeSales.get(key) + " oranges");
					}
					break;
				default:
					// Anything else is invalid
					System.out.println("Invalid Input");
				}
				break;
				
			case 2:	// Apples needed to order
				System.out.println("Please type the month by number (January is 1, February is 2, etc.)");
				int userMonthApple = scnr.nextInt();
				String userMonth = null;
				System.out.println("How many apples are on hand?");
				int userCountApple = scnr.nextInt();
				int applesNeeded = 0;
				switch(userMonthApple) {
				// We assign the user input to a string so we can query the dictionary
				case 1:
					userMonth = "January";
					break;
				case 2:
					userMonth = "February";
					break;
				case 3:
					userMonth = "March";
					break;
				case 4:
					userMonth = "April";
					break;
				case 5:
					userMonth = "May";
					break;
				case 6:
					userMonth = "June";
					break;
				case 7:
					userMonth = "July";
					break;
				case 8:
					userMonth = "August";
					break;
				case 9:
					userMonth = "September";
					break;
				case 10:
					userMonth = "October";
					break;
				case 11:
					userMonth = "November";
					break;
				case 12:
					userMonth = "December";
					break;
				}
				
				applesNeeded = (appleSales.get(userMonth));
				applesNeeded = applesNeeded - userCountApple;
				System.out.println("Oranges needed to order based on last years sales: " + applesNeeded);
		
				break;
				
			case 3:	// Oranges needed to order
				System.out.println("Please type the month by number (January is 1, February is 2, etc.)");
				int userMonthOrange = scnr.nextInt();
				userMonth = null;
				System.out.println("How many oranges are on hand?");
				userCountApple = scnr.nextInt();
				applesNeeded = 0;
				switch(userMonthOrange) {
				case 1:
					userMonth = "January";
					break;
				case 2:
					userMonth = "February";
					break;
				case 3:
					userMonth = "March";
					break;
				case 4:
					userMonth = "April";
					break;
				case 5:
					userMonth = "May";
					break;
				case 6:
					userMonth = "June";
					break;
				case 7:
					userMonth = "July";
					break;
				case 8:
					userMonth = "August";
					break;
				case 9:
					userMonth = "September";
					break;
				case 10:
					userMonth = "October";
					break;
				case 11:
					userMonth = "November";
					break;
				case 12:
					userMonth = "December";
					break;
				}
				
				applesNeeded = (orangeSales.get(userMonth));
				applesNeeded = applesNeeded - userCountApple;
				System.out.println("Oranges needed to order based on last years sales: " + applesNeeded);

				break;
				
			case 4:	// Quit
				// Say Goodbye to the user
				System.out.println("Closing program...");
				System.out.println("Goodbye");
				programRunning = false;
				break;
			default:
				System.out.println("Invalid Input");
			}
			
		}
		else {
				System.out.println("Goodbye");
			}

		scnr.close();
	}		
}
```


## Enhancement 3 Narrative: Databases
Narrative Three: Databases

**A.	Briefly describe the artifact. What is it? When was it created?**

The original artifact comes from CS-340 in the form of a text message expander, this program would take the user input of an abbreviation like “OMG, BRB, or OMW” and expands the message into the full text form of the message.  Originally, the program used a series of if-else statements to find a matching abbreviation, but I thought this would be a good place to implement a database.  I remade the program using Python and SQLite to give the program more complexity and to give it more tools to be successful.  Rather than using if-else statements to find the match, we will create SQL queries and run different queries depending on input.  
	
**B.	Justify the inclusion of the artifact in your ePortfolio. Why did you select this item? What specific components of the artifact showcase your skills and abilities in software development? How was the artifact improved?**

I selected this artifact because I thought it would be well suited to implement a database into, a database makes the program run smoother, adds complexity, and gives the user a lot more capability than the original program.  Databases are also easily exploitable, for this reason I designed the program with a security-first mindset in hopes to achieve: build on previous course outcomes as well as demonstrate my security first mindset that anticipates exploitation of my database (CS-499-05). The artifact now uses a database that the user can add additional abbreviations into and remove any old irrelevant abbreviations.  
	
**C.	Did you meet the course objectives you planned to meet with this enhancement in Module One? Do you have any updates to your outcome-coverage plans?**

This project has met the planned enhancements laid forth in Module One.  I wanted to implement a system where the user could preform CRUD operations on the data within the program, and implementing a database makes the most sense here.  Initially, I thought I would just make the main program, but I found that I needed to create some additional scripts for creating a new database locally and populating the database with common abbreviations, so those have been created as well.  I want to add some more depth to this program and maybe implement some other operations; ideally, I would like to find an online resource that contains abbreviations in a CSV file and populate the database with that data.  But for now, I have met my initial course objectives planned.
	
**D.	Reflect on the process of enhancing and/or modifying the artifact. What did you learn as you were creating it and improving it? What challenges did you face?**

I was never particularly good at working with databases, I think through my whole time at school, one of the only classes that I seriously struggled in was working with databases.  I knew the motions of how to get certain things to work, but I did not understand the full breadth of the information and I learned a lot creating this program.  One speed bump that I hit was taking user input and formatting it in a way that it would go into the database well, I spent a lot of time reading the SQLite documentation and I think it paid off.  The first function I made took me quite some time, the next one came together faster, and from there it was like I had been working with Python and SQLite my whole time here at school.  Once I had a deeper understanding of how SQLite input formatting worked, everything in the program seemed to start to fall in place.  

### Original Program
``` Java
import java.util.Scanner;

public class TextMsgExpander {
   
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in); // Initiate scanner for user input
        String textMessage; // This string will be where the user input is stored
        
        String BFF = "best friend forever"; // Initiate all the abbreviations in their unnabreviated form
        String IDK = "I don't know";
        String JK = "just kidding";
        String TMI = "too much information";
        String TTYL = "talk to you later";
       while (true) { //Program will loop until the user enters quit. 
    	   System.out.println("Enter text, or enter quit to quit."); // Ask user for input
    	   textMessage = scnr.nextLine();
    	   
    	   System.out.println("You entered: " + textMessage); // Output initial text message 
    	   System.out.println();
       
    	   // We only use if statements instead of if else statements. This way, if a text
    	   // contains multiple abbreviations to be expanded, they all execute
    	   if (textMessage.equalsIgnoreCase("quit")) { //If user enters quit, the program exits. It ignores casing
    		   System.out.println("Program is closing.");
    		   break;
    	   }
    	   if (textMessage.toUpperCase().contains("BFF")) {  // Test if text contains BFF; case matters for all of these!
    		   textMessage = textMessage.replace("BFF", BFF); // If so, replace with unabbreviated form
    		   System.out.println("Replaced \"BFF\" with " + "\"" + BFF + "\"" + ".");
    	   }
       
    	   if (textMessage.toUpperCase().contains("IDK")) { // Test ifq text contains IDK
    		   textMessage = textMessage.replace("IDK", IDK); // Replace with unabbreviated form
    		   System.out.println("Replaced \"IDK\" with " + "\"" + IDK + "\"" + ".");
    	   }
       
    	   if (textMessage.toUpperCase().contains("JK")) { // Test if text contains JK
    		   textMessage = textMessage.replace("JK", JK); // Replace with unabbreviated form
    		   System.out.println("Replaced \"JK\" with " + "\"" + JK + "\"" + ".");
    	   }
       
    	   if (textMessage.toUpperCase().contains("TMI")) { // Test if text contains TMI
    		   textMessage = textMessage.replace("TMI", TMI); // Replace with unabbreviated form
    		   System.out.println("Replaced \"TMI\" with " + "\"" + TMI + "\"" + ".");
    	   }
       
    	   if (textMessage.toUpperCase().contains("TTYL")) { // Test if text contains TTYL
    		   textMessage = textMessage.replace("TTYL", TTYL); // Replace with unabbreviated form
    		   System.out.println("Replaced \"TTYL\" with " + "\"" + TTYL + "\"" + ".");
    	   } 
       
    	   System.out.println(); 
    	   System.out.println("Expanded: " + textMessage); // Output the expanded text message
       }
    }
}
```
### New Program
``` Python
#!/usr/bin/python

import sqlite3

import cursor as cursor
import table as table

# This is an external dependency, may need to be installed via command line
from pip._vendor.distlib.compat import raw_input

# Connects to our database
conn = sqlite3.connect('test.db')

# Alias to clean up queries
c = conn.cursor()

# Output to ensure we opened DB correctly
print("Opened database successfully")


# Define a function to get data from DB
def get_data():     # Defining this as a function will make the queries look much cleaner
    with conn:
        c.execute("SELECT * FROM WORDS")


programRunning = True

# While there is user input, keep running
while programRunning:
    # Print a user Menu
    print("""
    1. Add new Abbreviation
    2. Delete Abbreviation
    3. Show Abbreviations
    4. Quit
    """)

    # Initialize variables to hold inputs
    ans = raw_input("Make a selection\n")
    user_input = "input"

    # Input 1 adds abbreviations
    if ans == "1":
        abrv = raw_input("What is the abbreviation?")
        result = c.fetchone()
        if result:
            # record already exists
            print("Record already exists")
        else:
            long = raw_input("What is the full phrase of the abbreviation?")
            # We need to structure the query to translate user inputs
            query = ('INSERT INTO WORDS (ABRV, Long) '
                     'VALUES (:ABRV, :Long);')
            # Add the parameter mask to the query
            params = {
                'ABRV': abrv,
                'Long': long
            }
            # Commit changes and close connection
            conn.commit()

        print("Abbreviation Added")

    # Input 2 deletes abbreviations
    elif ans == "2":
        # Prints abbreviations so user can see what is in the DB
        cursor = conn.execute("SELECT * from WORDS")
        print(cursor.fetchall())
        # Ask the user what they want to delete
        abrv = (raw_input("What abbreviation would you like to delete?:"),)
        # Ensure we have what the user wants to delete in the DB
        result = cursor.fetchone()

        # if we find the abbreviation delete it
        if result:
            query = ('DELETE from WORDS (ABRV) '
                     'VALUES (:ABRV);')
            # Add the parameter mask to the query
            params = {
                'ABRV': abrv
            }
            # Delete record
            conn.commit()
            print("Record deleted")
        else:
            # If we don't find a record, then it probably isn't there
            print("Abbreviation not present in database, try again.")

    # Input 3 prints out the abbreviations
    elif ans == "3":
        print("Abbreviation Found")
        cursor = conn.execute("SELECT * from WORDS")
        print(cursor.fetchall())

        conn.close()
    # Input 4 closes program
    elif ans == "4":
        print("Goodbye")
        # Set our boolean to false to close the program
        programRunning = False

    # Anything else is invalid
    elif ans != "":
        print("\n **Not Valid Choice, please try again**")
```
### Page Settings
You can use the [editor on GitHub](https://github.com/CalebHaley-SNHU/CalebHaley-SNHU.github.io/edit/main/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/CalebHaley-SNHU/CalebHaley-SNHU.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
