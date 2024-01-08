# Java-
TASK 1 Number Game
import java.util.Scanner;
public class NumberGame {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

	        // Scanner Class
	        Scanner sc = new Scanner(System.in);
	 
	        // Generate the numbers
	        int number = 1 + (int)(100
	                               * Math.random());
	 
	        // Given K trials
	        int K = 5;
	 
	        int i, guess;
	 
	        System.out.println(
	            "A number is chosen"
	            + " between 1 to 100."
	            + "Guess the number"
	            + " within 5 trials.");
	 
	        // Iterate over K Trials
	        for (i = 0; i < K; i++) {
	 
	            System.out.println(
	                "Guess the number:");
	 
	            // Take input for guessing
	            guess = sc.nextInt();
	 
	            // If the number is guessed
	            if (number == guess) {
	                System.out.println(
	                    "Congratulations!"
	                    + " You guessed the number.");
	                break;
	            }
	            else if (number > guess
	                     && i != K - 1) {
	                System.out.println(
	                    "The number is "
	                    + "greater than " + guess);
	            }
	            else if (number < guess
	                     && i != K - 1) {
	                System.out.println(
	                    "The number is"
	                    + " less than " + guess);
	            }
	        }
	 
	        if (i == K) {
	            System.out.println(
	                "You have exhausted"
	                + " K trials.");
	 
	            System.out.println(
	                "The number was " + number);
	        }
	    }
	 
	    // Driver Code
	    public static void
	    main(final String arg[])
	    {
	 
	        // Function Call
	        guessingNumberGame();
	    }
	}
Task-2 Calculator
 import java.util.Scanner;
public class  Calculator {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Scanner sc = new Scanner(System.in);
        char grade;
        System.out.println("Enter mark for subject English:");
        float math = sc.nextFloat();
        System.out.println("Enter mark for subject Java");
        float science=sc.nextFloat();
        System.out.println("Enter mark for subject Marathi");
        float marathi =sc.nextFloat();
        float total_marks= math+science+marathi;

        float average_percentage= total_marks/3;

        if(average_percentage>=90){
            grade='A';
        } else if (average_percentage>=80) {
            grade='B';

        } else if (average_percentage>=70) {
            grade='C';
        } else if (average_percentage>=60) {
           grade='D';
        } else if (average_percentage>=35) {
           grade='E';
        } else {
            grade='F';
        }
        System.out.println("\nResult:");
        System.out.println("Sum of marks obtained in all subjects="+total_marks);
        System.out.println("The sum of avearge is :"+average_percentage);
        System.out.println("Grade:"+grade);
	}

}

TASK 3 ATM interface

import java.util.HashMap;
import java.util.Scanner;

public class ATMinterface {
    public static void main(String[] args) {
        // install machine
        // creating object of class Atm_opn
        Atm_opn obj = new Atm_opn();
    }
}

class Data {
    // variables
    float Balance;
    String name;
    int pin;
    int transactions = 0;
    String transactionHistory = "";
}

class Atm_opn {

    Scanner sc = new Scanner(System.in);

    HashMap<String, Data> map = new HashMap<>();

    Atm_opn() {
        // constructor
        System.out.println("-------------------------------------------------------------------------------------------");
        System.out.println("\t\t\tGoliath National Bank - Your Financial Wingman");
        System.out.println("-------------------------------------------------------------------------------------------\n\n");
        System.out.println("Welcome to GNB Bank");
        opn();
    }

    public void opn() {
        System.out.print("Enter your Account Number: ");
        String AccNum = sc.next();
        try {
            if (map.containsKey(AccNum) == true) {
                Data obj = map.get(AccNum);
                Menu(obj);
            } else {
                System.out.println("Account Does not exist");
                System.out.println("-------------------------------------------------------------------------------------------\n\n");
                System.out.println("Kindly, create Bank Account first\n");
                System.out.print("Set your Bank Account Number: ");
                String AccNumber = sc.next();

                Data obj = new Data();
                map.put(AccNumber, obj);

                System.out.print("Enter your Name: ");
                obj.name = sc.next();

                System.out.print("Set your 4 digit pin : ");
                obj.pin = sc.nextInt();

                Menu(obj);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public void Menu(Data obj) {
        System.out.println("\n\n-------------------------------------------------------------------------------------------");

        System.out.println("Please Select a valid number ");

        System.out.println("1 . Check balance");
        System.out.println("2 . Deposit money");
        System.out.println("3 . Withdraw money");
        System.out.println("4 . Check another account");
        System.out.println("5 . Transfer money");
        System.out.println("6 . Transaction history");
        System.out.println("7 . exit");
        System.out.println("-------------------------------------------------------------------------------------------\n");

        System.out.print("Enter your choice: ");
        int x = sc.nextInt();
        System.out.println("");

        switch (x) {
            case 1: {
                check_Bal(obj);
                break;
            }
            case 2: {
                deposit(obj);
                break;
            }
            case 3: {
                withdraw(obj);
                break;
            }
            case 4: {
                opn();
                break;
            }
            case 5: {
                transfer(obj);
                break;
            }
            case 6: {
                transHistory(obj);
                break;
            }
            case 7: {
                System.out.println("Thank you!");
                break;
            }
            default: {
                System.out.println("Please enter a valid number: ");
                Menu(obj);
            }
        }
    }

    public void check_Bal(Data obj) {
        System.out.println("Your Bank Balance is: " + obj.Balance);
        Menu(obj);
    }

    public void deposit(Data obj) {
        System.out.print("Enter your amount to deposit: ");
        float a = sc.nextFloat();

        try {
            obj.Balance = obj.Balance + a;
            System.out.println("Amount deposited successfully");
            String str = a + " Rs deposited\n";
            obj.transactionHistory = obj.transactionHistory.concat(str);
            obj.transactions++;
            Menu(obj);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public void withdraw(Data obj) {
        System.out.print("Enter your amount to withdraw: ");
        float w = sc.nextFloat();

        try {
            if (obj.Balance >= w) {
                obj.Balance = obj.Balance - w;
                System.out.println("Amount withdrawn successfully");
                String str = w + " Rs Withdrawn\n";
                obj.transactionHistory = obj.transactionHistory.concat(str);
                obj.transactions++;
            } else {
                System.out.println("Insufficient Balance\nEnter a valid number to withdraw\n");
                withdraw(obj);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

        Menu(obj);
    }

    public void transfer(Data obj) {
        System.out.println("Enter amount to transfer");
        float trans = sc.nextFloat();

        try {
            if (trans == 0) {
                System.out.println("Transfer amount cannot be Null/0");
            }

            if (obj.Balance >= trans) {
                obj.Balance = obj.Balance - trans;
            } else {
                System.out.println("Insufficient Balance");
                transfer(obj);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        Amount_trans(trans);
    }

    public void Amount_trans(float trans) {
        System.out.print("Enter Account Number of the recipient to transfer amount: ");
        String AccNum = sc.next();

        try {
            if (map.containsKey(AccNum) == true) {
                Data obj = map.get(AccNum);

                obj.Balance = obj.Balance + trans;
                System.out.println("Amount transfer successfully to " + obj.name);
                obj.transactions++;
                String str = trans + " Rs transferred to " + obj.name + "\n";
                obj.transactionHistory = obj.transactionHistory.concat(str);

                Menu(obj);
            } else {
                System.out.println("Account of the recipient does not exist");

                System.out.println("Kindly, create Bank Account first\n");

                System.out.print("Set your Bank Account Number: ");
                String AccNumber = sc.next();

                Data obj = new Data();
                map.put(AccNumber, obj);

                System.out.print("Enter your Name: ");
                obj.name = sc.next();

                System.out.print("Set your 4 digit pin : ");
                obj.pin = sc.nextInt();

                obj.Balance = obj.Balance + trans;
                System.out.println("Amount transfer successfully");
                obj.transactions++;
                String str = trans + " Rs transferred to " + obj.name + "\n";
                obj.transactionHistory = obj.transactionHistory.concat(str);
                Menu(obj);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public void transHistory(Data obj) {
        if (obj.transactions == 0) {
            System.out.println("\n You had no transactions.");
            Menu(obj);
        } else {
            System.out.println("\n" + obj.transactionHistory);
            Menu(obj);
        }
    }
}
