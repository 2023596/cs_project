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


