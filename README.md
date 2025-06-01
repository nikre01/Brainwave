 package atmapp;

import java.util.Scanner;

public class ATM2 {
    // Predefined credentials for login
    private static final String savedUsername = "@Nikki";
    private static final String savedPassword = "#Nikitadhakar";
    private static final String correctPin = "5421";

    private static double balance = 10000.0;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("====== Welcome to Nikki's' Java ATM ======");
        System.out.println("----- Login Page -----");

        // Step 1: Login Page
        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.print("Enter username: ");
        String inputUsername = sc.nextLine();

        System.out.print("Enter password: ");
        String inputPassword = sc.nextLine();

        if (!inputUsername.equals(savedUsername) || !inputPassword.equals(savedPassword)) {
            System.out.println("Login failed! Invalid username or password.");
            sc.close();
            return;
        }

        System.out.println("Login successful! Welcome, " + name + ".");

        // Step 2: PIN Check
        System.out.print("Enter your 4-digit PIN: ");
        String userPin = sc.nextLine();

        if (!userPin.equals(correctPin)) {
            System.out.println("Incorrect PIN! Access denied.");
            sc.close();
            return;
        }

        // Step 3: ATM Menu
        int choice;
        do {
            System.out.println("\n--- ATM Menu ---");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Exit");

            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    checkBalance();
                    break;
                case 2:
                    deposit(sc);
                    break;
                case 3:
                    withdraw(sc);
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM, " + name + "! Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }

        } while (choice != 4);

        sc.close();
    }

    public static void checkBalance() {
        System.out.printf("Your current balance is: ₹%.2f%n", balance);
    }

    public static void deposit(Scanner sc) {
        System.out.print("Enter amount to deposit: ₹");
        double amount = sc.nextDouble();

        if (amount <= 0) {
            System.out.println("Deposit amount must be positive.");
        } else {
            balance += amount;
            System.out.printf("₹%.2f deposited successfully.%n", amount);
        }
    }

    public static void withdraw(Scanner sc) {
        System.out.print("Enter amount to withdraw: ₹");
        double amount = sc.nextDouble();

        if (amount <= 0) {
            System.out.println("Withdraw amount must be positive.");
        } else if (amount > balance) {
            System.out.println("Insufficient balance.");
        } else {
            balance -= amount;
            System.out.printf("₹%.2f withdrawn successfully.%n", amount);
        }
    }
}
