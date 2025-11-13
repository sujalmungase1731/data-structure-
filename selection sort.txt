#include <iostream>
using namespace std;
void selectionSort(float arr[], int n) {
    for(int i = 0; i < n-1; i++) {
        int minIndex = i;
        for(int j = i+1; j < n; j++) {
            if(arr[j] < arr[minIndex])
                minIndex = j;
        }
        float temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
}
int main() {
    int n;
    cout << "Enter total number of students: ";
    cin >> n;
    float per[n];
    cout << "Enter percentages:\n";
    for(int i = 0; i < n; i++)
        cin >> per[i];
    selectionSort(per, n);
    cout << "\nTop 5 scores are:\n";
    for(int i = n-1; i >= max(0, n-5); i--)
        cout << per[i] << " ";
    return 0;
}