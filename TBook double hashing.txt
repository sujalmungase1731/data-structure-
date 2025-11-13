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
    int hash1(long key) {
        return key % SIZE;
    }
    int hash2(long key) {
        return 7 - (key % 7); 
    }
    void insert(long key) {
        int index = hash1(key);
        int step = hash2(key);
        while(phone[index] != -1) {
            index = (index + step) % SIZE;
        }
        phone[index] = key;
    }
    void search(long key) {
        int index = hash1(key);
        int step = hash2(key);
        int start = index;
        while(phone[index] != key) {
            index = (index + step) % SIZE;
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
    cout << "Enter phone numbers:\n";
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