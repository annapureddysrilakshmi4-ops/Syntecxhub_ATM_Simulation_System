# Syntecxhub_ATM_Simulation_System
import java.util.Scanner;


class ATM {

   
    private int originalPin;
    private double balance;
    private boolean sessionActive;

    // Constructor
    ATM(int pin, double balance) {

        this.originalPin = pin;
        this.balance = balance;
        this.sessionActive = true;
    }

    // PIN Verification
    public boolean verifyPin(int enteredPin) {

        return enteredPin == originalPin;
    }

    // Balance Check
    public void checkBalance() {

        System.out.println("Current Balance: ₹" + balance);
    }

    // Deposit Money
    public void deposit(double amount) {

        if(amount > 0) {

            balance += amount;

            System.out.println("₹" + amount + " Deposited Successfully!");

        } else {

            System.out.println("Invalid Deposit Amount!");
        }
    }

    // Withdraw Money
    public void withdraw(double amount) {

        if(amount <= balance) {

            balance -= amount;

            System.out.println("Please Collect Your Cash");
            System.out.println("Remaining Balance: ₹" + balance);

        } else {

            System.out.println("Insufficient Balance!");
        }
    }

    // Exit ATM
    public void exitATM() {

        sessionActive = false;

        System.out.println("Session Ended Successfully!");
        System.out.println("Thank You For Using ATM");
    }

    // Start ATM
    public void startATM() {

        Scanner sc = new Scanner(System.in);

        // FIRST PAGE → PIN ENTRY
        System.out.println("\n===== ATM MACHINE =====");

        boolean pinVerified = false;

        // Ask PIN until correct PIN entered
        while(!pinVerified) {

            System.out.print("Enter ATM PIN: ");

            int enteredPin = sc.nextInt();

            // Verify PIN
            if(verifyPin(enteredPin)) {

                pinVerified = true;

                System.out.println("\nPIN Verified Successfully!");

            } else {

                System.out.println("Invalid PIN!");
                System.out.println("Please Enter the Correct PIN.\n");
            }
        }

        int choice;

        
        while(sessionActive) {

            System.out.println("\n===== ATM MENU =====");

            System.out.println("1. Balance Check");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Exit");

            System.out.print("Enter Your Choice: ");

            choice = sc.nextInt();

            switch(choice) {

                case 1:

                    checkBalance();

                    break;

                case 2:

                    System.out.print("Enter Deposit Amount: ₹");

                    double depositAmount = sc.nextDouble();

                    deposit(depositAmount);

                    break;

                case 3:

                    System.out.print("Enter Withdrawal Amount: ₹");

                    double withdrawAmount = sc.nextDouble();

                    withdraw(withdrawAmount);

                    break;

                case 4:

                    exitATM();

                    break;

                default:

                    System.out.println("Invalid Choice!");
            }
        }
    }
}

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

    
        System.out.print("Set Your ATM PIN: ");

        int userPin = sc.nextInt();

      
        System.out.print("Enter Initial Balance: ₹");

        double initialBalance = sc.nextDouble();

       
        ATM userATM = new ATM(userPin, initialBalance);

        
        userATM.startATM();
    }
}