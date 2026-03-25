import java.util.Scanner;

abstract class account {
    long Accnumber;
    String name;
    String Branch_name;
    String IFSC;
    long phnum;
    double balance;

    account(long Accnumber, String name, String Branch_name, String IFSC, long phnum, double balance) {
        this.Accnumber = Accnumber;
        this.name = name;
        this.Branch_name = Branch_name;
        this.IFSC = IFSC;
        this.phnum = phnum;
        this.balance = balance;
    }

    abstract void deposit(double amt);
    abstract void withdraw(double amt);

    
    void transfer(account receiver, double amt) {
        if (amt <= balance) {
            this.balance -= amt;
            receiver.balance += amt;
            System.out.println("Transfer successful!");
        } else {
            System.out.println("Insufficient balance");
        }
    }


    void transferBank(String newBank, String newIFSC) {
        System.out.println("Account transferring from " + Branch_name + " to " + newBank);

        this.Branch_name = newBank;
        this.IFSC = newIFSC;

        System.out.println("Account transferred successfully!");
    }

    
    void showDetails() {
        System.out.println("\n--- Account Details ---");
        System.out.println("Account No: " + Accnumber);
        System.out.println("Name: " + name);
        System.out.println("Bank: " + Branch_name);
        System.out.println("IFSC: " + IFSC);
        System.out.println("Phone: " + phnum);
        System.out.println("Balance: " + balance);
    }
}

class Bank extends account {

    Bank(long Accnumber, String name, String Branch_name, String IFSC, long phnum, double balance) {
        super(Accnumber, name, Branch_name, IFSC, phnum, balance);
    }

    public void deposit(double amt) {
        balance += amt;
        System.out.println("Deposited: " + amt);
    }

    public void withdraw(double amt) {
        if (amt <= balance) {
            balance -= amt;
            System.out.println("Withdrawn: " + amt);
        } else {
            System.out.println("Insufficient balance");
        }
    }
}

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        Bank b1 = new Bank(101, "RAM", "SBI", "SBI0001", 9876543210L, 5000);
        Bank b2 = new Bank(102, "SHYAM", "HDFC", "HDFC0002", 9123456780L, 3000);

        int choice;

        do {
            System.out.println("\n1.Deposit 2.Withdraw 3.Transfer Money 4.Transfer Bank 5.Show Details 6.Exit");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter amount: ");
                    b1.deposit(sc.nextDouble());
                    break;

                case 2:
                    System.out.print("Enter amount: ");
                    b1.withdraw(sc.nextDouble());
                    break;

                case 3:
                    System.out.print("Enter amount: ");
                    b1.transfer(b2, sc.nextDouble());
                    break;

                case 4:
                    sc.nextLine();
                    System.out.print("Enter new bank: ");
                    String nb = sc.nextLine();
                    System.out.print("Enter IFSC: ");
                    String ni = sc.nextLine();
                    b1.transferBank(nb, ni);
                    break;

                case 5:
                    b1.showDetails();
                    break;

                case 6:
                    System.out.println("Exit");
                    break;

                default:
                    System.out.println("Invalid choice");
            }

        } while (choice != 6);
 
    }
}
