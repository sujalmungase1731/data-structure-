#include <iostream>
using namespace std;
class Node {
public:
    int seat;           
    int status;         
    Node *next, *prev;
};
class Cinema {
public:
    Node *row[10];      
    Cinema() {
        for(int i = 0; i < 10; i++) {
            row[i] = NULL;
            Node *prev = NULL;
            for(int j = 1; j <= 7; j++) {
                Node *temp = new Node();
                temp->seat = j;
                temp->status = rand() % 2;  
                temp->next = NULL;
                temp->prev = prev;
                if(prev != NULL) prev->next = temp;
                else row[i] = temp;
                prev = temp;
            }
        }
    }
    void displayAvailable() {
        cout << "\nAvailable Seats (0 = Free, 1 = Booked):\n";
        for(int i = 0; i < 10; i++) {
            cout << "Row " << i+1 << " : ";
            Node *t = row[i];
            while(t != NULL) {
                cout << "[" << t->seat << ":" << t->status << "] ";
                t = t->next;
            }
            cout << endl;
        }
    }
    void cancelSeat(int r, int s) {
        if(r < 1 || r > 10 || s < 1 || s > 7) {
            cout << "Invalid seat!\n";
            return;
        }
        Node *t = row[r-1];
        while(t != NULL && t->seat != s)
            t = t->next;
        if(t != NULL && t->status == 1) {
            t->status = 0;
            cout << "\nSeat Cancelled Successfully!\n";
        } else {
            cout << "\nSeat is already free or invalid.\n";
        }
    }
};
int main() {
    Cinema c;
    int ch, r, s;
    do {
        cout << "\n----- Cinema Ticket System -----\n";
        cout << "1. Display Available Seats\n";
        cout << "2. Cancel a Booking\n";
        cout << "Enter choice: ";
        cin >> ch;
        switch(ch) {
            case 1:
                c.displayAvailable();
                break;
            case 2:
                cout << "Enter Row (1-10): ";
                cin >> r;
                cout << "Enter Seat (1-7): ";
                cin >> s;
                c.cancelSeat(r, s);
                break;
            case 3:
                break;
        }
    } while(ch != 3);
    return 0;
}