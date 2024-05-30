#include <iostream>
#include <fstream>
#include <string>
#include<iomanip>
#include <stdlib.h>
#include<windows.h>

using namespace std;

const int MAX_BAKERY_ITEMS = 10;
const int MAX_SALES = 10;

struct BakeryItem {
    int id;
    string name;
    double price;
};

struct S
{
    int value;
};

struct Sale {
    int id;
    string customerName;
    BakeryItem items[10]; // Array to store bakery items in a sale
    int itemCount; // Number of items in the sale
    double totalAmount;
};

// User login credentials
const string username = "Anushka";
const string password = "1111";

// Function prototypes
void displayMenu();
bool login();
void viewBakeryItems(BakeryItem items[], int itemCount);
void manageBakeryItems(BakeryItem items[], int& itemCount);
void manageSales(Sale sales[], int& saleCount, BakeryItem items[], int itemCount);
void viewCompanyDetails();
void logout();
void saveSalesToFile(Sale sales[], int saleCount);
void loadSalesFromFile(Sale sales[], int& saleCount);
void saveBakeryItemsToFile(BakeryItem items[], int itemCount);
void loadBakeryItemsFromFile(BakeryItem items[], int& itemCount);

// Global variables
Sale sales[MAX_SALES]; // Array to store sales
int saleCount = 0;
BakeryItem bakeryItems[MAX_BAKERY_ITEMS]; // Array to store bakery items
int itemCount = 0;

int main() {
    // Load existing sales data and bakery items from files
    loadSalesFromFile(sales, saleCount);
    loadBakeryItemsFromFile(bakeryItems, itemCount);

    S s{ 3 };


    // User login
    if (!login()) {
        cout << "            Login failed. Exiting the program." << endl<< endl;
        exit( 3 );
        return 1;
    }

    while (true) {
        system("color 05 ");
        displayMenu();

        int choice;
        cout << "Enter your choice: ";
        cin >> choice;
        cout << endl;

        switch (choice) {
            case 1:
                void loadBakeryItemsFromFile(BakeryItem items[], int& itemCount);
                viewBakeryItems(bakeryItems, itemCount);
                break;
            case 2:
                manageBakeryItems(bakeryItems, itemCount);
                void saveBakeryItemsToFile(BakeryItem items[], int itemCount);
                break;
            case 3:
                manageSales(sales, saleCount, bakeryItems, itemCount);
                void saveSalesToFile(Sale sales[], int saleCount);
                break;
            case 4:
                viewCompanyDetails();
                void loadSalesFromFile(Sale sales[], int& saleCount);
                break;
            case 5:
                logout();
                break;
            case 6:
                // Save data and exit
                saveSalesToFile(sales, saleCount);
                saveBakeryItemsToFile(bakeryItems, itemCount);
                cout << endl<< "Exiting the program." << endl<< endl;
                cout << "**********THANK YOU FOR USING OUR SYSTEM**********" << endl<< endl;
                exit( 3 );
                //break;
            default:
                cout << "Invalid choice. Please try again." << endl<< endl;
        }
    }

    return 0;
}

void displayMenu() {
    cout<<endl;
    cout << "***********************************************************************************************************************" << endl;
    cout<<endl;
    cout << "Amber Bakery Automated Billing System" << endl;
    cout << "=====================================" << endl<< endl;
    cout << "1. View Bakery Items" << endl;
    cout << "2. Manage Bakery Items" << endl;
    cout << "3. Manage Sales" << endl;
    cout << "4. View Sales Details" << endl;
    cout << "5. Logout" << endl;
    cout << "6. Exit" << endl<<endl;
}

bool login() {
    string enteredUsername, enteredPassword;

    cout << "           Please enter your username : ";
    cin >> enteredUsername;

    cout << "           Please enter your password : ";
    cin >> enteredPassword;

    if (enteredUsername == username && enteredPassword == password) {
        cout << endl;
        cout << "           Login successful. Welcome, " << username << "!" << endl;
        system("color 04 ");
        return true;
    } else {
        cout << endl<< "            Login failed. Incorrect username or password." << endl;
        exit( 3 );
        return false;
    }
}

void viewBakeryItems(BakeryItem items[], int itemCount) {
    cout << "Bakery Items:" << endl;
    for (int i = 0; i < itemCount; i++) {
        cout << "ID: " << items[i].id << "|Name: " << items[i].name << "|Price: " << items[i].price << endl;
    }
}

void manageBakeryItems(BakeryItem items[], int& itemCount) {
        int id;
        string name;
        float price;

        cout<<" Enter item ID number  : ";
        cin>>id;
        cout<<" Enter item name       : ";
        cin>>name;
        cout<<" Enter item price      : ";
        cin>>price;

        fstream x;
        x.open("bakery_items.txt",ios::app);
        x<<id<<setw(14)<<name<<setw(12)<<price<<setw(17)<<endl;
        x.close();
}

void manageSales(Sale sales[], int& saleCount, BakeryItem items[], int itemCount) {
        int id;
        string customerName;
        float totalAmount;

        cout<<" Enter item ID number     : ";
        cin>>id;
        cout<<" Enter item customer name : ";
        cin>>customerName;
        cout<<" Enter item total amount  : ";
        cin>>totalAmount;

        fstream x;
        x.open("sales.txt",ios::app);
        x<<id<<setw(14)<<customerName<<setw(12)<<totalAmount<<setw(17)<<endl;
        x.close();
}

void viewCompanyDetails() {
    cout<<"        AMBER BAKERS "<<endl;
    cout<<"        ------------- "<<endl;
    cout<<"Address    : Units 9-11, Portland Commercial Estate, Ripple Road, Barking, Essex, IG11 0TW . "<<endl;
    cout<<"Telephone  : +44 (0)20 85175533, +44 (0)78 60701991 "<<endl;
    cout<<"E Mail     : sales@amberbakery.co.uk "<<endl;
    cout<<"Open Hours : Weekdays 7.00 am - 8.00 pm"<<endl;
    cout<<"           : Weekends 6.30 am - 10.30 pm"<<endl;
}

void logout() {

    cout << "Logged out. Goodbye!" << endl;

    loadSalesFromFile(sales, saleCount);
    loadBakeryItemsFromFile(bakeryItems, itemCount);

    // User login
    if (!login()) {
        cout << "           --Please Try Again--" << endl<< endl;
        //return 1;
    }

    while (true) {
        system("color 09 ");
        displayMenu();

        int choice;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                void loadBakeryItemsFromFile(BakeryItem items[], int& itemCount);
                viewBakeryItems(bakeryItems, itemCount);
                break;
            case 2:
                manageBakeryItems(bakeryItems, itemCount);
                void saveBakeryItemsToFile(BakeryItem items[], int itemCount);
                break;
            case 3:
                manageSales(sales, saleCount, bakeryItems, itemCount);
                void saveSalesToFile(Sale sales[], int saleCount);
                break;
            case 4:
                viewCompanyDetails();
                void loadSalesFromFile(Sale sales[], int& saleCount);
                break;
            case 5:
                logout();
                break;
            case 6:
                saveSalesToFile(sales, saleCount);
                saveBakeryItemsToFile(bakeryItems, itemCount);
                cout << "Exiting the program." << endl<< endl;
                cout << "***************THANK YOU FOR USING OUR SYSTEM***************" << endl<< endl;
                exit( 3 );
            default:
                cout << "Invalid Value, Please Try Again." << endl<< endl;
                cout << endl<< endl;
        }
    }
}

void saveSalesToFile(Sale sales[], int saleCount) {
    ofstream file("sales.txt");
    if (file.is_open()) {
        for (int i = 0; i < saleCount; i++) {
            file << "Sale ID: " << sales[i].id << endl;
            file << "Customer Name: " << sales[i].customerName << endl;
            file << "Total Amount: $" << sales[i].totalAmount << endl;
            file << "Items:" << endl;
            for (int j = 0; j < sales[i].itemCount; j++) {
                file << "  - Name: " << sales[i].items[j].name << " | Price: $" << sales[i].items[j].price << endl;
            }
            file << endl;
        }
        file.close();
        cout<<endl;
        cout << "Sales data saved to 'sales.txt'." <<endl;
    } else {
        cerr << "Error: Unable to save sales data to file." <<endl;
    }
}

void loadSalesFromFile(Sale sales[], int& saleCount) {
    ifstream file("sales.txt");
    if (file.is_open()) {
        Sale sale;
        while (file >> sale.id) {
            file.ignore();
            getline(file, sale.customerName);
            file >> sale.totalAmount;
            file.ignore();
            sale.itemCount = 0;
            string line;
            while (getline(file, line) && !line.empty() && sale.itemCount < 10) {
                BakeryItem item;
                file.ignore(11); // Skip "Name: "
                getline(file, item.name, '|');
                file.ignore(10); // Skip "Price: $"
                file >> item.price;
                file.ignore();
                sale.items[sale.itemCount++] = item;
            }
            sales[saleCount++] = sale;
        }
        file.close();
        cout << "Sales data loaded from 'sales.txt'." <<endl;
    } else {
        cerr << "Warning: 'sales.txt' not found. No sales data loaded." <<endl;
    }
}

void saveBakeryItemsToFile(BakeryItem items[], int itemCount) {
    ofstream file("bakery_items.txt");
    if (file.is_open()) {
        for (int i = 0; i < itemCount; i++) {
            file << "ID: " << items[i].id << " | Name: " << items[i].name << " | Price: $" << items[i].price << endl;
        }
        file.close();
        cout << "Bakery items data saved to 'bakery_items.txt'." << endl;
    } else {
        cerr << "Error: Unable to save bakery items data to file." <<endl;
    }
}

void loadBakeryItemsFromFile(BakeryItem items[], int& itemCount) {
    ifstream file("bakery_items.txt");
    if (file.is_open()) {
        BakeryItem item;
        while (file >> item.id) {
            file.ignore();
            getline(file, item.name, '|');
            file >> item.price;
            file.ignore();
            items[itemCount++] = item;
        }
        file.close();
        cout << "Bakery items data loaded from 'bakery_items.txt'." << endl<< endl;
    } else {
        cerr << "Warning: 'bakery_items.txt' not found. No bakery items data loaded." << endl<<endl;
    }
}
