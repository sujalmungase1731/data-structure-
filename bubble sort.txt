#include <iostream>
using namespace std;
void bubbleSort(float arr[], int n) {
    for(int i = 0; i < n-1; i++) {
        for(int j = 0; j < n-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                float temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
int main() {
    int n;
    cout << "Enter number of students: ";
    cin >> n;
    float per[n];
    cout << "Enter percentages:\n";
    for(int i = 0; i < n; i++)
        cin >> per[i];
    bubbleSort(per, n);
    cout << "\nTop 5 Scores:\n";
    int count = 0;
    for(int i = n-1; i >= 0 && count < 5; i--) {
        cout << per[i] << " ";
        count++;
    }
    return 0;
}