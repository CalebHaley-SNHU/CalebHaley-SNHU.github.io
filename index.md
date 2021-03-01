# Welcome to Caleb Haley's GitHub Page
On this page, I will be demonstrating some of my skills developed over the course of my at SNHU in three formats: Software Design and Engineering, Algorithms and Data Structure, and Databases.  I will be taking older assignments and enhancing them in some way or another each week.  Ultimately, my goal is for each narrative to work with each other to build a well functioning system.

## Enhancement 1 Narrative: Software Design and Engineering
For this narrative, I will be taking an assignment that was originally a Zoo monitoring system which would read a text file about the data and give the user a warning if there is an issue with the habitat.  I want to redeign this application to compliment the second narrative. I want to modify this program to read data about wood pellets, which will be saved in a text file.  With this application, I want to see quick information about each brand which will be pulled from multiple text files.  I then want to give the user a warning if inventory on any item is low.
```
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


## Enhancement 2 Narrative: Algorithms and Data Structure
For the second narrative, I will be modifying one of the first programs made here at SNHU.  This is a Java program that would ask the user for how much fruit they should order, based on what the user inputs.  I would like modify this to meet a real world application of mine, I would like to predict the amount of wood pellets to order for a retailer given the temperature outside.  We typically sit down with a pen and paper to calculate this, but I believe this application could be modified to remove the need for human calculation and a user could have the data they need in seconds.  This is from IT-145
```
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

## Enhancement 3 Narrative: Databases
For the third narrative, I would like to implement a database on a Text Message Expander created in CS340.  This program would take string input from the user and match it using if statements and a hard comparisson.  I would like to put a database of different text messages that can be expanded, simplifying the program and adding functionality.
```
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
