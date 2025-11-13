#include <iostream>
#include <string>
using namespace std;
class Node {
public:
    string name;
    long long prn;
    Node* next;
    Node(string n, long long p) {
        name = n;
        prn = p;
        next = NULL;
    }
};
class Club {
    Node* head;
public:
    Club() { head = NULL; }
    void addPresident(string name, long long prn) {
        Node* n = new Node(name, prn);
        n->next = head;
        head = n;
        cout << "President added!\n";
    }
    void addMember(string name, long long prn) {
        if (!head) { cout << "Add President first!\n"; return; }
        Node* n = new Node(name, prn);
        Node* temp = head;
        while (temp->next && temp->next->next)
            temp = temp->next;
        n->next = temp->next;
        temp->next = n;
        cout << "Member added!\n";
    }
    void addSecretary(string name, long long prn) {
        Node* n = new Node(name, prn);
        if (!head) head = n;
        else {
            Node* temp = head;
            while (temp->next) temp = temp->next;
            temp->next = n;
        }
        cout << "Secretary added!\n";
    }
    void display() {
        if (!head) { cout << "No members yet!\n"; return; }
        Node* temp = head;
        cout << "\n--- Pinnacle Club Members ---\n";
        while (temp) {
            if (temp == head)
                cout << "President -> ";
            else if (temp->next == NULL)
                cout << "Secretary -> ";
            else
                cout << "Member -> ";
            cout << temp->name << " (" << temp->prn << ")\n";
            temp = temp->next;
        }
    }
    void countMembers() {
        int c = 0;
        Node* t = head;
        while (t) { c++; t = t->next; }
        cout << "\nTotal Members: " << c << endl;
    }
};
int main() {
    Club c;
    int ch;
    string name;
    long long prn;
    do {
        cout << "\n===== Pinnacle Club Menu =====";
        cout << "\n1. Add President";
        cout << "\n2. Add Member";
        cout << "\n3. Add Secretary";
        cout << "\n4. Display Members";
        cout << "\n5. Count Members";
        cout << "\n6. Exit";
        cout << "\nEnter your choice: ";
        cin >> ch;
        switch (ch) {
            case 1:
                cout << "Enter President Name: ";
                cin.ignore();
                getline(cin, name);
                cout << "Enter PRN: ";
                cin >> prn;
                c.addPresident(name, prn);
                break;
            case 2:
                cout << "Enter Member Name: ";
                cin.ignore();
                getline(cin, name);
                cout << "Enter PRN: ";
                cin >> prn;
                c.addMember(name, prn);
                break;
            case 3:
                cout << "Enter Secretary Name: ";
                cin.ignore();
                getline(cin, name);
                cout << "Enter PRN: ";
                cin >> prn;
                c.addSecretary(name, prn);
                break;
            case 4:
                c.display();
                break;
            case 5:
                c.countMembers();
                break;
            case 6:
                cout << "Exiting... Thank you!\n";
                break;
            default:
                cout << "Invalid choice!\n";
        }
    } while (ch != 6);
    return 0;
}