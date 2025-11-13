#include <iostream>
using namespace std;
int main() {
    int n, key;
    cout << "Enter number of students: ";
    cin >> n;
    int roll[n];
    cout << "Enter roll numbers: ";
    for (int i = 0; i < n; i++)
        cin >> roll[i];
    cout << "Enter roll number to search: ";
    cin >> key;
    for (int i = 0; i < n; i++) {
        if (roll[i] == key) {
            cout<<"Student attended the training program."<<endl;
            return 0;
        }
    }
    cout << "Student did not attend the training program."<<endl;
return 0;
}
