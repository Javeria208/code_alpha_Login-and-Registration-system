
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

void createUserFile(const string& username, const string& password) {
    ofstream userFile(username + ".txt");  
    if (userFile.is_open()) {
        userFile << password; 
        userFile.close();  
        cout << "User file created successfully!" << endl;
    } else {
        cout << "Error creating user file." << endl;
    }
}


void registerUser() 
{
    string username, password;

    cout << "Enter username: ";
    cin >> username;

    cout << "Enter password: ";
    cin >> password;

    // Check if file already exists
    ifstream file(username + ".txt");
    if (file.good()) 
    {
        cout << "Username already taken!" << endl;
        return;
    }
    file.close();

    // Create user file
    createUserFile(username, password);
}

// if user file exists
bool userFileExists(const string& username) 
{
    ifstream file(username + ".txt");
    return file.good();
}

//  log in a user
void loginUser()
{
    string username, password, storedPassword;

    cout << "Enter username: ";
    cin >> username;

    cout << "Enter password: ";
    cin >> password;

    // Check if file exists
    if (!userFileExists(username)) 
    {
        cout << "Username does not exist!" << endl;
        return;
    }

    // Read stored password from file
    ifstream file(username + ".txt");
    getline(file, storedPassword);
    file.close();

    if (password == storedPassword) 
    {
        cout << "Login successful!" << endl;
    } else {
        cout << "Incorrect password!" << endl;
    }
}

int main()
{
    int choice;

    cout << "1. Register" << endl;
    cout << "2. Login" << endl;
    cout << "Enter choice: ";
    cin >> choice;

    switch (choice)
    {
        case 1:
            registerUser();
            break;
        case 2:
            loginUser();
            break;
        default:
            cout << "Invalid choice!" << endl;
    }

    return 0;
}
