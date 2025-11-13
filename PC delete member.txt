#include <iostream>
using namespace std;

struct Student {
    int prn;
    string name;
    Student* next;
    Student(int p, string n) {
        prn = p;
        name = n;
        next = NULL;
    }
};

class PinnacleClub {
    Student* head;
public:
    PinnacleClub() { head = NULL; }

    void addMember(int prn, string name) {
        Student* newNode = new Student(prn, name);
        if (head == NULL)
            head = newNode;
        else {
            Student* temp = head;
            while (temp->next != NULL)
                temp = temp->next;
            temp->next = newNode;
        }
    }

    void deleteMember(int prn) {
        if (head == NULL) {
            cout << "List is empty.\n";
            return;
  }
        if (head->prn == prn) {
            Student* t = head;
            head = head->next;
            delete t;
            cout << "President with PRN " << prn << " deleted.\n";
            return;
        }
        Student* temp = head;
        while (temp->next != NULL && temp->next->prn != prn)
            temp = temp->next;
        if (temp->next == NULL) {
            cout << "Member not found.\n";
            return;
        }
        Student* del = temp->next;
        temp->next = del->next;
        delete del;
        cout << "Member with PRN " << prn << " deleted.\n";
    }

    void display() {
        if (head == NULL) {
            cout << "No members in club.\n";
            return;
        }
        cout << "\nClub Members:\n";
        Student* temp = head;
        while (temp != NULL) {
            cout << temp->prn << " - " << temp->name << endl;
            temp = temp->next;
        }
    }

    void concatenate(PinnacleClub &obj) {
        if (head == NULL) {
            head = obj.head;
            return;
        }
        Student* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = obj.head;
    }
};

int main() {
    PinnacleClub divA, divB;
    int n, prn;
    string name;

    cout << "Enter number of members in Division A: ";
    cin >> n;
    for (int i = 0; i < n; i++) {
        cout << "Enter PRN and Name: ";
        cin >> prn >> name;
        divA.addMember(prn, name);
    }

    cout << "\nEnter number of members in Division B: ";
    cin >> n;
    for (int i = 0; i < n; i++) {
        cout << "Enter PRN and Name: ";
        cin >> prn >> name;
        divB.addMember(prn, name);
    }

    cout << "\n--- Division A ---";
    divA.display();
    cout << "\n--- Division B ---";
    divB.display();

    cout << "\nEnter PRN to delete from Division A: ";
    cin >> prn;
    divA.deleteMember(prn);

    cout << "\nAfter deletion, Division A:";
    divA.display();

    cout << "\nConcatenating Division B into Division A...\n";
    divA.concatenate(divB);

    cout << "\n--- Final Combined List ---";
    divA.display();

    return 0;
}