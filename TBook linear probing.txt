#include <iostream>
using namespace std;
#define SIZE 10
class HashTable {
    long phone[SIZE];
public:
    HashTable() {
        for(int i = 0; i < SIZE; i++)
            phone[i] = -1;
    }
    int hash(long key) {
        return key % SIZE;
    }
    void insert(long key) {
        int index = hash(key);
        while(phone[index] != -1) {
            index = (index + 1) % SIZE; 
        }
        phone[index] = key;
    }
    void search(long key) {
        int index = hash(key);
        int start = index;
        while(phone[index] != key) {
            index = (index + 1) % SIZE;
            if(index == start) {
                cout << "Number NOT found.\n";
                return;
            }
        }
        cout << "Number FOUND at index " << index << endl;
    }
    void display() {
        cout << "\nHash Table:\n";
        for(int i = 0; i < SIZE; i++)
            cout << i << " --> " << phone[i] << endl;
    }
};
int main() {
    HashTable ht;
    int n;
    long num;
    cout << "Enter number of clients: ";
    cin >> n;
    cout << "Enter Phone Numbers:\n";
    for(int i = 0; i < n; i++) {
        cin >> num;
        ht.insert(num);
    }
    ht.display();
    cout << "\nEnter number to search: ";
    cin >> num;
    ht.search(num);
    return 0;
}