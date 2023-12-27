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
        cout << "Goal cannot be higher than current balance." << endl;
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

