import java.util.Scanner;
import java.util.HashMap;

class Account {
    private String name;
    private String accountNumber;
    private String phoneNumber;
    private String password;
    private double balance;

    public Account(String name, String accountNumber, String phoneNumber, String password) {
        this.name = name;
        this.accountNumber = accountNumber;
        this.phoneNumber = phoneNumber;
        this.password = password;
        this.balance = 0.0;
    }

    public String getName() {
        return name;
    } 

    public String getAccountNumber() {
        return accountNumber;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public boolean authenticate(String phoneNumber, String password) {
        return this.phoneNumber.equals(phoneNumber) && this.password.equals(password);
    }

    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: " + amount);
        System.out.println("Current Balance: " + balance);
    }

    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
            System.out.println("Current Balance: " + balance);
        } else {
            System.out.println("Insufficient Balance");
        }
    }

    public void displayBalance() {
        System.out.println("Name: " + name);
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Balance: " + balance);
    }
}

public class BankingManagementSystem {
    private static HashMap<String, Account> accounts = new HashMap<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Menu
        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Login");
            System.out.println("2. Register");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    login(scanner);
                    break;
                case 2:
                    register(scanner);
                    break;
                case 3:
                    System.out.println("Exiting...");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice");
            }
        }
    }

    private static void login(Scanner scanner) {
        System.out.print("Enter Phone Number: ");
        String phoneNumber = scanner.next();
        System.out.print("Enter Password: ");
        String password = scanner.next();

        if (accounts.containsKey(phoneNumber)) {
            Account account = accounts.get(phoneNumber);
            if (account.authenticate(phoneNumber, password)) {
                System.out.println("Login Successful");
                displayMenu(scanner, account);
            } else {
                System.out.println("Invalid Password");
            }
        } else {
            System.out.println("Account not found");
        }
    }

    private static void register(Scanner scanner) {
        System.out.print("Enter Name: ");
        String name = scanner.next();
        System.out.print("Enter Phone Number: ");
        String phoneNumber = scanner.next();
        System.out.print("Enter Password: ");
        String password = scanner.next();
        System.out.print("Enter Account Number: ");
        String accountNumber = scanner.next();

        if (!accounts.containsKey(phoneNumber)) {
            Account account = new Account(name, accountNumber, phoneNumber, password);
            accounts.put(phoneNumber, account);
            System.out.println("Registration Successful");
        } else {
            System.out.println("Account already exists");
        }
    }

    private static void displayMenu(Scanner scanner, Account account) {
        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Check Balance");
            System.out.println("4. Logout");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    break;
                case 2:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    account.withdraw(withdrawAmount);
                    break;
                case 3:
                        account.displayBalance();
                        break;
                    case 4:
                        System.out.println("Exiting...");
                        System.exit(0);
                    default:
                        System.out.println("Invalid choice");
                }
            
        }
    }
}
