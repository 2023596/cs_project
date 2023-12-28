#include <iostream>
#include <string>
using namespace std;

struct Transaction {
    double amount;
};
void setBudgetGoal(double amount, double& goal) {
    cout << "Enter your savings goal: $";
    cin >> goal;

    cout << "Your savings goal: $" << goal << endl;

    if (goal > amount) {
        cout << "Goal cannot be higher than Current balance." << endl;
    } else {
        cout << "Goal set successfully!" << endl;
    }
}
int login() {
    string login = "user123";
    string pass = "pass123";
    string inputUsername, inputPassword;

    cout << "USERNAME:";
    cin >> inputUsername;
    cout << "PASSWORD:";
    cin >> inputPassword;

    return (inputUsername == login && inputPassword == pass);
}
void displayMenu() {
   
    cout << "1. Add Transaction" << endl;
    cout << "2. View Transactions" << endl;
     cout << "3. Analyze Data" << endl;
    cout << "4. Set Budget Goal" << endl;
    cout << "5. Withdrawal" << endl;
    cout << "6. Exit" << endl;
    cout << "Enter your choice: ";
    cout<<"\n";
}

void addTransaction(Transaction transactions[], int& count, double& currentBalance) {
    int numTransactions;
    cout << "Enter the number of transactions you want to add: ";
    cin >> numTransactions;

    for (int i = 0; i < numTransactions; ++i) {
        if (count < 100) {
            Transaction newTransaction;
            cout << "Enter transaction amount: $";
            cin >> newTransaction.amount;
            transactions[count++] = newTransaction;
            currentBalance += newTransaction.amount; // Update the current balance
            cout << "Transaction added successfully!" << endl;
        } else {
            cout << "Transaction limit reached!" << endl;
            break;
        }
    }
}

void withdrawal(Transaction transactions[], int& count, double& currentBalance, double goal) {
    int numWithdrawals;
    cout << "Enter the number of withdrawals you want to make: ";
    cin >> numWithdrawals;

    for (int i = 0; i < numWithdrawals; ++i) {
        double amount;
        cout << "Enter the amount to withdraw: $";
        cin >> amount;
        
        if (goal > 0 && amount > goal) {
            cout << "WARNING: YOUR WITHDRAWAL MAY AFFECT YOUR SAVINGS GOAL!" << endl;
            cout << "HOWEVER, THE WITHDRAWAL HAS BEEN APPROVED AS PER YOUR REQUEST." << endl; 
        }

        if (amount <= currentBalance) {
            Transaction newTransaction;
            newTransaction.amount = -amount; // Represent withdrawal as a negative amount
            transactions[count++] = newTransaction;
            currentBalance -= amount; // Update the current balance
            cout << "Withdrawal successful!" << endl;
        } else {
            cout << "Withdrawal amount exceeds the current balance. The transaction will proceed." << endl;
            break;
        }
    }
}

void viewTransactions(Transaction transactions[], int count) {
	int a=1;
    cout << "Transactions:" << endl;
    for (int i = 0; i < count; i++) {
        cout << "Transaction Amount "<< a++<<":" << transactions[i].amount << endl;
    }
}

void analyzeData(Transaction transactions[], int count, double currentBalance) {
    cout << "Performing data analysis..." << endl;

    if (count > 0) {
        cout << "Transaction History:" << endl;
        for (int i = 0; i < count; ++i) {
            cout << "Transaction Amount: " << transactions[i].amount << endl;
        }
    } else {
        cout << "No transactions to analyze." << endl;
    }

    double totalDeposits = 0.0;
    double totalWithdrawals = 0.0;
    for (int i = 0; i < count; ++i) {
        if (transactions[i].amount > 0) {
            totalDeposits += transactions[i].amount;
        } else {
            totalWithdrawals += transactions[i].amount;
        }
    }

    cout << "Total Deposits: $" << totalDeposits << endl;
    cout << "Total Withdrawals: $" << totalWithdrawals << endl;
    cout << "Remaining Balance: $" << currentBalance << endl;
}

int main() {
    bool isLoggedIn = login();
    if (isLoggedIn) {
        Transaction transactions[100];
        int transactionCount = 0;
        double currentBalance = 0.0;
        double savingsGoal = 0.0;
        int choice;
           cout<<"****PERSONAL FINANCE DASHBOARD****";
            do {
        	cout<<"\n";

        
            displayMenu();
            cin >> choice;

            switch (choice) {
                case 1:
                    addTransaction(transactions, transactionCount, currentBalance);
                    break;
                case 2:
                    viewTransactions(transactions, transactionCount);
                    break;
                case 3:
                    analyzeData(transactions, transactionCount, currentBalance);
                    break;
                case 4:
                    setBudgetGoal(currentBalance, savingsGoal);
                    break;
                case 5:
                    withdrawal(transactions, transactionCount, currentBalance, savingsGoal);
                    break;
                case 6:
                    cout << "Exiting the program. Thank you!" << endl;
                    break;
                default:
                    cout << "Invalid choice. Please enter a valid option." << endl;
                    break;
            }
        } while (choice != 6);
    } else {
        cout << "Login failed" << endl;
    }
    return 0;
}

