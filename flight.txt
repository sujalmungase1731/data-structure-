#include <iostream>
#include <list>
#include <queue>
using namespace std;

class Graph {
    int V;
    list<int>* adj;

public:
    Graph(int V) {
        this->V = V;
        adj = new list<int>[V];
    }

    void addEdge(int v, int w) {
        if (v >= 0 && v < V && w >= 0 && w < V) {
            adj[v].push_back(w);
            adj[w].push_back(v);
            cout << "Connection added successfully.\n";
        } else {
            cout << "Invalid city index! Please enter between 0 and " << V - 1 << ".\n";
        }
    }

    void display(string cities[]) {
        cout << "\nFlight Path Graph (Adjacency List):\n";
        for (int i = 0; i < V; i++) {
            cout << cities[i] << " -> ";
            for (int x : adj[i])
                cout << cities[x] << " ";
            cout << endl;
        }
    }

    void BFS(int start, bool visited[]) {
        queue<int> q;
        visited[start] = true;
        q.push(start);
        while (!q.empty()) {
            int u = q.front();
            q.pop();
            for (int v : adj[u]) {
                if (!visited[v]) {
                    visited[v] = true;
                    q.push(v);
                }
            }
        }
    }

    bool isConnected() {
        bool* visited = new bool[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;
        BFS(0, visited);
        for (int i = 0; i < V; i++)
            if (!visited[i])
                return false;
        return true;
    }
};

int main() {
    int V, E;
    cout << "Enter number of cities: ";
    cin >> V;

    string* cities = new string[V];
    cout << "Enter city names:\n";
    for (int i = 0; i < V; i++)
        cin >> cities[i];

    Graph g(V);

    cout << "Enter number of flight connections: ";
    cin >> E;

    cout << "Enter connections (city1_index city2_index):\n";
    cout << "(Valid indices are 0 to " << V - 1 << ")\n";
    for (int i = 0; i < E; i++) {
        int a, b;
        cin >> a >> b;
        g.addEdge(a, b);
    }

    g.display(cities);

    if (g.isConnected())
        cout << "\nGraph is Connected (All cities reachable)\n";
    else
        cout << "\nGraph is Not Connected\n";

    return 0;
}


