/**
 * importing all the java functions requires to run the code
 * @author Mphephu Makhadzi
 */

import java.util.*;
import java.io.File;
import java.io.FileNotFoundException;

/**
 * the main class of the toktik application
 * @author Mphephu Makhadzi
 */

public class TokTik{

    /**
     * the main method for the app is static and void because it does not return and output
     * uses binary search tree with the parameter account and post from the account class and the post class
     * uses scanner to allow the class to utilise user inputs
     * brings out the user menu and allows the user to select an option
     * int choice is used to indicate that the user input will be a number
     * @author Mphephu Makhadzi
     */

    public static void main (String arg []){
        BinarySearchTree<Account> bt = new BinarySearchTree<Account>();
        BinarySearchTree<Post> pst = new BinarySearchTree<Post> ();
      
         Scanner input = new Scanner(System.in);

         /*testing     
          Account acc = new Account("Makhadzi", "Best developer alive!");
      bt.insert(acc);
      acc.addPost(new Post("Psot title", "Video.p3", 475));
      acc.addPost(new Post("the say", "Pictures.p3", 75));
      acc.addPost(new Post("Ps", "asdfg.p3", 777));
      
      bt.insert(new Account("Zyon", "Im here"));
      bt.insert(new Account("Maximus", "Can't stop me"));
      bt.insert(new Account("Caleb", "so? what now?"));*/

        System.out.println("Choose an action from menu:");
        System.out.println("1. Find the profile description for a given account");
        System.out.println("2. List all accounts");
        System.out.println("3. Create an account");
        System.out.println("4. Delete an account");
        System.out.println("5. Display all posts for a single account");
        System.out.println("6. Add a new post for an account");
        System.out.println("7. Load a file of actions from disk and process this");
        System.out.println("8. Quit");
        System.out.print("Enter your choice:");
        int choice = input.nextInt();
        
        /**
             * while loop used to include run switch cases when choice is not option 8
             * switch allows the user to select an option and runs that option based on the case number
             * switch uses the choice input to run the cases
             * @author Mphephu Makhadzi
             */
            
        while(choice != 8){
            
            switch(choice){

                /**
                 * first case to run when the user selects option 1
                 * the system requires the user to enter the account name, it uses that input with is a string to find the account
                 * the input is used to create a constructor
                 * the system then looks for the account using an if statement, if the account is available in the binary tree dataset, the system will print out the description of the profile name that has been selected
                 * an else statement notifies the user that the account is not available if the if statement does not run
                 * break is used to end the case and to avoid running an infinite loop
                 * @author Mphephu Makhadzi
                 */
                
                case 1:
                System.out.print("Enter the account name: ");
                String accName = input.next();
                Account look = new Account(accName, " ");
                if (bt.find(look) != null){
                    System.out.println("The profile description is: " + bt.find(look).data.description);
                }

                else{
                    System.out.println("Account name not available! \nCreate new account\n");
                }
                break;
                
                /**
                 * this runs when the user selects option 2
                 * it alerts the user that all the accounts in the dataset will be listed
                 * the list is generated from the binary tree and uses the inOrder method to list all the accounts
                 * breaks stops the case from running when it is done, avoids an infinite loop
                 * @author Mphephu Makhadzi
                 */

                case 2:
                System.out.println("List of created accounts: ");
                bt.inOrder();

                break;

                /**
                 * runs when the user selects option 3 to create and account that is not included in the dataset
                 * it requires a name from the user and saves it as a tring as well as the description for the account being created
                 * it uses the insert method to add the account and description that the user put in
                 * this alerts the user that the account has been created once this is done
                 * the case breaks and ends 
                 * @author Mphephu Makhadzi
                 */

                case 3:
                System.out.print("Enter the account name: "); 
                String nameAcc = input.next();
                System.out.print("Enter description: ");
                String junk = input.next();
                String descr = input.nextLine();
                
                bt.insert(new Account(nameAcc, descr));
                System.out.println("Your account has been created!\n");

                break;

                /**
                 * runs when user selects option 8 to delete an account
                 * requires the user to put in the account name using the system.out.print method
                 * uses the input to create a parameter for the if statement
                 * the if statement runs if the name the user put in exits
                 * uses the find method to find the account and uses the find as the parameter for the delete method
                 * it alerts the user that the account has been created once this is done
                 * the else statement runs when the account name does not exits and alerts the user of this
                 * the case breaks and ends
                 * @author Mphephu Makhadzi
                 */

                case 4:
                System.out.print("Enter the account name: "); 
                String nameOfAcc = input.next();
                if (bt.find(new Account(nameOfAcc, " ")) != null){
                    bt.delete(bt.find(new Account(nameOfAcc, " ")).data);
                    System.out.println("Your account has been deleted!");
                
                }

                else{
                    System.out.println("Account name not available! \nCreate new account\n");
                }

                break;

                /**
                 * runs then the user selects option 5 to get all the posts of the account
                 * uses the print method to request the account name and stores it into a string
                 * an if statement runs using the find method if the account is available
                 * the find method is then used to get all posts from the dataset using the getPost method from the post class
                 * the else statement runs when the account name provided does not exist
                 * the case ends when the break statement runs
                 */

                case 5:
                System.out.print("Enter the account name: "); 
                String nameAccount = input.next();
                if (bt.find(new Account(nameAccount, " ")) != null){
                    bt.find(new Account(nameAccount, " ")).data.getPost();
                }

                else{
                    System.out.println("Account name not available! \nCreate new account\n");
                }

                break;

                /**
                 * runs when the user selects option 6 to add a post
                 * print method used to alert the user that the account name, title and video details are required and saved as a string
                 * an if statement runs using the find method to find the account that the post is being added to if the account exists
                 * the addPost method is used to add the post to the account that was found using the input provided
                 * the else statement runs if the account does not exist
                 * the case ends when break runs
                 * @author Mphephu Makhadzi
                 */

                case 6: 
                System.out.print("Enter the account name: "); 
                String nameAccount1 = input.next();
                System.out.print("Enter post title: ");
                junk = input.next();
                String postTitle = input.nextLine();
                System.out.print("Enter video details: ");
                String vidDits = input.next();
                System.out.println("Yout video has been uploaded!");
                if (bt.find(new Account(nameAccount1, " ")) != null){
                    bt.find(new Account(nameAccount1, " ")).data.addPost(new Post(postTitle, vidDits, 0));
                }

                else{
                    System.out.println("Account name not available! \nCreate new account\n");
                }

                break;

                /**
                 * runs when user selects option 7 to insert a file into the code to create or add accounts using the dataset.txt file
                 * print method used to request the fine name and create a constructor to access the file \
                 * file reader method reads the file and then runs the while loop
                 * the if statement runs if the statement of the text file starts with create and creates accounts using the names and description provided in the text file
                 * the insert method add the account into the account class
                 * the else if statement runs when the data in the file starts with add and adds a post to the post class to the account mentioned
                 * when it is successful is alerts the user and closes the file
                 * the catch method detects if the system cannot read the file and prints the statement in the print method
                 * the default is run if the option chosen is not part of the cases
                 * the system breaks
                 * @author Mphephu Makhadzi
                 */

                case 7:
                try {
                    System.out.print("Enter the file in name{txt} format: ");
                    String file = input.next();
                    File dataFolder= new File(file);

               Scanner fileReader = new Scanner(dataFolder);

               while (fileReader.hasNextLine()) {
                String nameAcc1,descriPtion;
                String data = fileReader.nextLine();

                  if (data.startsWith("Create")){
                      String accountData = data.substring(7);
                      nameAcc1 = accountData.substring(0,accountData.indexOf(" "));
                      descriPtion = accountData.substring(accountData.indexOf(" "),accountData.length());
                      bt.insert(new Account(nameAcc1,descriPtion));
                    }

                  else if (data.startsWith("Add")){
                     String postData = data.substring(4);
                     nameAcc1 = postData.substring(0,postData.indexOf(" "));
                     String otherPost= postData.substring(postData.indexOf(" "), postData.length());
                     otherPost = otherPost.substring(1, otherPost.length());
                     String videoName = otherPost.substring(0,otherPost.indexOf(" "));
                     String otherPost1 = otherPost.substring(0,otherPost.indexOf(" "));
                     String titleOfPost = otherPost1.substring(otherPost1.indexOf(" ")+1,otherPost1.length());           
                   }
               }
              
               System.out.println("Accounts have been added!");
               fileReader.close();
              
                } 
                catch (FileNotFoundException e){
                System.out.println("Error!");
                e.printStackTrace();
                }

                break;

            default:
                System.out.println("Input not available, choose available options in menu!"); 

              }
            
            System.out.println("Choose an action from menu:");
            System.out.println("1. Find the profile description for a given account");
            System.out.println("2. List all accounts");
            System.out.println("3. Create an account");
            System.out.println("4. Delete an account");
            System.out.println("5. Display all posts for a single account");
            System.out.println("6. Add a new post for an account");
            System.out.println("7. Load a file of actions from disk and process this");
            System.out.println("8. Quit");
            System.out.print("Enter your choice:");
            choice = input.nextInt(); 

            }
            
        }
        
    }
