#include <iostream>
#include <string>
#include <vector>
#include <fstream>
using namespace std;

class Product {
public:
    string name;
    float price;
    int quantity;
    Product(string name, float price, int quantity) {
        this->name = name;
        this->price = price;
        this->quantity = quantity;
    }
};

class Customer {
public:
    string name;
    float budget;
    Customer(string name, float budget) {
        this->name = name;
        this->budget = budget;
    }

    bool makeOrder(Product product, int quantity) {
        if (product.quantity < quantity) {
            cout << "Недостатньо товару на складі." << endl;
            return false;
        }
        if (product.price * quantity > budget) {
            cout << "Недостатньо коштів для здійснення покупки." << endl;
            return false;
        }
        product.quantity -= quantity;
        budget -= product.price * quantity;
        cout << "Покупка " << product.name << " (" << quantity << " шт.) проведена успішно. Витрачено: " << product.price * quantity << ". Залишок на рахунку: " << budget << "." << endl;
        return true;
    }
};

class Store {
public:
    vector<Product> products;
    void addProduct(string name, float price, int quantity) {
        Product product(name, price, quantity);
        products.push_back(product);
    }

    Product findProduct(string name) {
        for (int i = 0; i < products.size(); i++) {
            if (products[i].name == name) {
                return products[i];
            }
        }
        return Product("", 0, 0);
    }
};

class BlackList {
public:
    vector<Customer> customers;
    void addCustomer(Customer customer) {
        customers.push_back(customer);
        cout << "Покупець " << customer.name << " доданий до чорного списку." << endl;

        ofstream blacklistFile; // створюємо об'єкт для запису в файл
        blacklistFile.open("blacklist.txt", ios::app); // відкриваємо файл для додавання даних в кінець

        if (blacklistFile.is_open()) { // перевіряємо, чи відкрито файл
            blacklistFile << customer.name << endl; // записуємо ім'я клієнта в файл
            blacklistFile.close(); // закриваємо файл
        } else {
            cout << "Помилка відкриття файлу." << endl;
        }
    }

    bool checkCustomer(Customer customer) {
        for (int i = 0; i < customers.size(); i++) {
            if (customers[i].name == customer.name) {
                return true;
            }
        }
        return false;
    }
};

int main() {
    Store store;
    store.addProduct("Телефон", 10000, 10);
    store.addProduct("Ноутбук", 20000, 5);

    // виводимо список товарів у вигляді меню
    cout << "Виберіть товар:" << endl;
    for (int i = 0; i < store.products.size(); i++) {
        cout << i + 1 << ". " << store.products[i].name << " - Ціна: " << store.products[i].price << ", Кількість: " << store.products[i].quantity << endl;
    }

    Customer customer("Олег", 1500000);

    cout << "Покупець " << customer.name << ". Бюджет: " << customer.budget << "." << endl;

    int choice;
    cout << "Виберіть товар (1-" << store.products.size() << "): ";
    cin >> choice;

    if (choice < 1 || choice > store.products.size()) {
        cout << "Ви вибрали неіснуючий товар." << endl;
        return 0;
    }

    Product product = store.products[choice - 1];

    if (!customer.makeOrder(product, 2)) {
        BlackList blackList;
        blackList.addCustomer(customer);
    }

    return 0;
}

