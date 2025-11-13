#include <iostream>
using namespace std;
#define MAX 5  
class JobQueue {
    int queue[MAX];
    int front, rear;
public:
    JobQueue() {
        front = -1;
        rear = -1;
    }
    void addJob(int jobID) {
        if (rear == MAX - 1) {
            cout << "Queue is full. Cannot add job.\n";
            return;
        }
        if (front == -1) front = 0;
        rear++;
        queue[rear] = jobID;
        cout << "Job " << jobID << " added.\n";
    }
    void deleteJob() {
        if (front == -1 || front > rear) {
            cout << "Queue is empty. No job to delete.\n";
            return;
        }
        cout << "Job " << queue[front] << " deleted.\n";
        front++;
    }
};
int main() {
    JobQueue jq;
    int choice, jobID;  
    for (int i = 0; i < 5; i++) {
        cout << "\n1. Add Job\n2. Delete Job\nEnter your choice: ";
        cin >> choice;
        if (choice == 1) {
            cout << "Enter Job ID: ";
            cin >> jobID;
            jq.addJob(jobID);
        } else if (choice == 2) {
            jq.deleteJob();
        } else {
            cout << "Invalid choice.\n";
        }
    }
    return 0;
}