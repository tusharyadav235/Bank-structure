//# Bank-structure
// program of Bank Structureimport java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class BankAccount {
    private String bankName;
    private Map<String, Account> accounts;

    public BankAccount(String bankName) {
        this.bankName = bankName;
        this.accounts = new HashMap<>();
    }

    public void createAccount(String accountNumber, String accountHolderName) {
        if (accounts.containsKey(accountNumber)) {
            System.out.println("Account number already exists.");
        } else {
            Account account = new Account(accountHolderName);
            accounts.put(accountNumber, account);
            System.out.println("Account created successfully.");
        }
    }

    public void deposit(String accountNumber, double amount) {
        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            account.deposit(amount);
        } else {
            System.out.println("Account number not found.");
        }
    }

    public void checkBalance(String accountNumber) {
        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            account.checkBalance();
        } else {
            System.out.println("Account number not found.");
        }
    }

    public void withdraw(String accountNumber, double amount) {
        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            account.withdraw(amount);
        } else {
            System.out.println("Account number not found.");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Welcome to the  Bank of CORRUPTION: ");
        String bankName = scanner.nextLine();
        if (bankName.isEmpty()) {
            bankName = "Bank of USA";
        }

        BankAccount bank = new BankAccount(bankName);

        while (true) {
            System.out.println("1. Create Account");
            System.out.println("2. Deposit");
            System.out.println("3. Check Balance");
            System.out.println("4. Withdraw");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();
            scanner.nextLine();

            switch (option) {
                case 1:
                    System.out.print("Enter account number: ");
                    String accountNumber = scanner.nextLine();
                    System.out.print("Enter account holder name: ");
                    String accountHolderName = scanner.nextLine();
                    bank.createAccount(accountNumber, accountHolderName);
                    break;
                case 2:
                    System.out.print("Enter account number: ");
                    accountNumber = scanner.nextLine();
                    System.out.print("Enter deposit amount: ");
                    double depositAmount = scanner.nextDouble();
                    scanner.nextLine(); 
                    bank.deposit(accountNumber, depositAmount);
                    break;
                case 3:
                    System.out.print("Enter account number: ");
                    accountNumber = scanner.nextLine();
                    bank.checkBalance(accountNumber);
                    break;
                case 4:
                    System.out.print("Enter account number: ");
                    accountNumber = scanner.nextLine();
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawalAmount = scanner.nextDouble();
                    scanner.nextLine(); 
                    bank.withdraw(accountNumber, withdrawalAmount);
                    break;
                case 5:
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    private static class Account {
        private String accountHolderName;
        private double balance;

        public Account(String accountHolderName) {
            this.accountHolderName = accountHolderName;
            this.balance = 0.0;
        }

        public void deposit(double amount) {
            balance += amount;
            System.out.println("Deposit successful. New balance: $" + balance);
        }

        public void checkBalance() {
            System.out.println("Current balance: $" + balance);
        }

        public void withdraw(double amount) {
            if (amount > balance) {
                System.out.println("You don't have sufficient balance.");
            } else {
                balance -= amount;
                System.out.println("Withdrawal successful. New balance: $" + balance);
            }
        }
    }
}


 
