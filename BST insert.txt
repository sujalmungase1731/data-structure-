#include <iostream>  
#include <limits>    
#include <algorithm> 
using namespace std;
struct Node {
    int data;       
    Node* left;     
    Node* right;    
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};
Node* insert(Node* root, int val) {
    if (root == nullptr) {
        cout << "Node with value " << val << " inserted." << endl;
        return new Node(val); 
    }
    if (val < root->data) {
        root->left = insert(root->left, val);
    }
    else if (val > root->data) {
        root->right = insert(root->right, val);
    }
    else {
        cout << "Value " << val << " already exists in the tree. Not inserting duplicate." << endl;
    }
    return root; 
}
int longestPathNodes(Node* root) {
    if (root == nullptr) {
        return 0; 
    }
    int leftHeight = longestPathNodes(root->left);
    int rightHeight = longestPathNodes(root->right);
    return 1 + max(leftHeight, rightHeight); 
}
int findMinimum(Node* root) {
    if (root == nullptr) {
        cerr << "Tree is empty. Cannot find minimum." << endl;
        return -1; 
    }
    Node* current = root;
    while (current->left != nullptr) {
        current = current->left;
    }
    return current->data;
}
void mirrorTree(Node* root) {
    if (root == nullptr) {
        return; 
    }
    mirrorTree(root->left);
    mirrorTree(root->right);
    Node* temp = root->left;
    root->left = root->right;
    root->right = temp;
}
bool search(Node* root, int val) {
    if (root == nullptr) {
        return false;
    }
    if (root->data == val) {
        return true;
    }
    if (val < root->data) {
        return search(root->left, val);
    }
    else {
        return search(root->right, val);
    }
}
void displayTree(Node* node) {
    if (node == nullptr) {
        return;
    }
    cout << node->data << " ";       
    displayTree(node->left);         
    displayTree(node->right);        
}
void deleteTree(Node* node) {
    if (node == nullptr) {
        return;
    }
    deleteTree(node->left);  
    deleteTree(node->right); 
    delete node;            
}
void displayMenu() {
    cout << "\n--- Binary Search Tree Operations ---" << endl;
    cout << "1. Insert a new node" << endl;
    cout << "2. Find number of nodes in longest path from root" << endl;
    cout << "3. Find minimum data value" << endl;
    cout << "Enter your choice: ";
}
int main() {
    Node* root = nullptr; 
    cout << "--- Initial Tree Construction ---" << endl;
    cout << "Enter values to insert into the initial tree (enter -999 to stop):" << endl;
    int initialValue;
    while (true) {
        cout << "Enter value: ";
        cin >> initialValue;
        while (cin.fail()) {
            cout << "Invalid input. Please enter an integer: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cin >> initialValue;
        }
        if (initialValue == -999) {
            break;
        }
        root = insert(root, initialValue);
    }
    int choice;
    int value;
    do {
        displayMenu();
        cin >> choice;
        while (cin.fail()) {
            cout << "Invalid input. Please enter a number from the menu: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n'); 
            cin >> choice;
        }
        switch (choice) {
            case 1:
                cout << "Enter value to insert: ";
                cin >> value;
                while (cin.fail()) {
                    cout << "Invalid input. Please enter an integer: ";
                    cin.clear();
                    cin.ignore(numeric_limits<streamsize>::max(), '\n');
                    cin >> value;
                }
                root = insert(root, value);
                break;
            case 2: 
                cout << "Number of nodes in longest path from root: " << longestPathNodes(root) << endl;
                break;
            case 3: 
                cout << "Minimum data value in the tree: " << findMinimum(root) << endl;
                break;
            default: 
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 3); 
    deleteTree(root);
    root = nullptr; 
    return 0; 
}

