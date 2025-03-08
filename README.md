# CodeAplha_LoginandRegistration_system

#include <iostream>
#include <fstream>
#include <string>
#include <sstream>
using namespace std;

class User {
private:
    string username;
    string password;

public:

    User(string u, string p) : username(u), password(p) {}

 
    string getUsername() const {
        return username;
    }

    string getPassword() const {
        return password;
    }


    void registerUser() {
    
        ofstream file(username + ".txt");
        if (file.is_open()) {
            file << username << endl;
            file << password << endl;
            file.close();
            cout << "Registration successful! User file created." << endl;
        } else {
            cout << "Error creating user file." << endl;
        }
    }


    static bool loginUser() {
        string username, password;
        cout << "Enter your username: ";
        cin >> username;
        cout << "Enter your password: ";
        cin >> password;

        ifstream file(username + ".txt");
        if (!file.is_open()) {
            cout << "No such user found!" << endl;
            return false;
        }

        string storedUsername, storedPassword;
        getline(file, storedUsername);
        getline(file, storedPassword);
        file.close();

        if (storedUsername == username && storedPassword == password) {
            cout << "Login successful!" << endl;
            return true;
        } else {
            cout << "Incorrect username or password!" << endl;
            return false;
        }
    }
};


void displayMenu() {
    int choice;
    while (true) {
        cout << "1. Register\n";
        cout << "2. Login\n";
        cout << "3. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        if (choice == 1) {
            string username, password;
            cout << "Enter a username: ";
            cin >> username;
            cout << "Enter a password: ";
            cin >> password;
            User newUser(username, password);
            newUser.registerUser();
        } else if (choice == 2) {
            if (User::loginUser()) {
                break;  
            }
        } else if (choice == 3) {
            break; 
        } else {
            cout << "Invalid choice! Please try again." << endl;
        }
    }
}

int main() {
    displayMenu();
    return 0;
}
