#include <iostream>
#include <stack>
using namespace std;
bool isMatching(char open, char close) {
    return (open == '(' && close == ')') ||
           (open == '{' && close == '}') ||
           (open == '[' && close == ']');
}
bool isBalanced(const string &exp) {
    stack<char> st;
    for(char ch : exp) {
        if(ch == '(' || ch == '{' || ch == '[') {
            st.push(ch);
        } else if(ch == ')' || ch == '}' || ch == ']') {
            if(st.empty()) return false;            
            char top = st.top(); st.pop();
            if(!isMatching(top, ch)) return false;  
        }
        
    }
    return st.empty();
}
int main() {
    string exp;
    cout << "Enter expression: ";
    getline(cin, exp);
    if(isBalanced(exp))
        cout << "Expression is WELL PARENTHESIZED.\n";
    else
        cout << "Expression is NOT WELL PARENTHESIZED.\n";
    return 0;
}