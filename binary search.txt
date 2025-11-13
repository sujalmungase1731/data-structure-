#include <iostream>
using namespace std;
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == key)
            return 1;
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return 0;
}
int main() {
    int n, key;
    cout << "Enter number of students: ";
    cin >> n;
    int roll[n];
    cout << "Enter roll numbers in sorted order: ";
    for (int i = 0; i < n; i++)
        cin >> roll[i];
    cout << "Enter roll number to search: ";
    cin >> key;
    if (binarySearch(roll, n, key))
        cout << "Student attended the training program.";
    else
        cout << "Student did not attend the training program.";
}