# CODSOFT
Internship
import java.util.Scanner;
// Step 4: BankAccount class
class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public double checkBalance() {
        return balance;
    }

    public boolean deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            return true;
        }
        return false;
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }
}

// Step 1 & 2: ATM class and interface
public class ATM {
    private BankAccount account;
    private Scanner scanner;

    public ATM(BankAccount account) {
        this.account = account;
        this.scanner = new Scanner(System.in);
    }

    public void start() {
        System.out.println("Welcome to the ATM Machine!");
        int choice;

        do {
            System.out.println("\nPlease select an option:");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Exit");

            System.out.print("Enter choice (1-4): ");
            while (!scanner.hasNextInt()) {
                System.out.print("Invalid input. Please enter a number (1-4): ");
                scanner.next(); // discard invalid input
            }

            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    checkBalance();
                    break;
                case 2:
                    deposit();
                    break;
                case 3:
                    withdraw();
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid option. Please choose between 1 and 4.");
            }
        } while (choice != 4);

        scanner.close();
    }

    // Step 3: ATM operation methods
    private void checkBalance() {
        System.out.printf("Your current balance is: $%.2f%n", account.checkBalance());
    }

    private void deposit() {
        System.out.print("Enter amount to deposit: $");
        double amount = scanner.nextDouble();
        if (account.deposit(amount)) {
            System.out.printf("Successfully deposited $%.2f%n", amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    private void withdraw() {
        System.out.print("Enter amount to withdraw: $");
        double amount = scanner.nextDouble();
        if (account.withdraw(amount)) {
            System.out.printf("Successfully withdrew $%.2f%n", amount);
        } else {
            System.out.println("Insufficient funds or invalid amount.");
        }
    }

    // Step 7: main method to run the program
    public static void main(String[] args) {
        // Step 5: Connect BankAccount to ATM
        BankAccount userAccount = new BankAccount(1000.0); // initial balance
        ATM atmMachine = new ATM(userAccount);
        atmMachine.start();
    }
}
