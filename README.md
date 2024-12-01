#include <iostream>
#include <vector>
#include <queue>
#include <algorithm> 

using namespace std;

const int MAX = 100005;
vector<int> adj[MAX];
int parent[MAX];

void bfs(int n) {
    queue<int> q;
    q.push(1);
    parent[1] = -1; 

    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (int v : adj[u]) {
            if (parent[v] == 0) { 
                parent[v] = u;
                q.push(v);
                if (v == n) return; 
            }
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m;
    for (int i = 0; i < m; ++i) {
        int a, b;
        cin >> a >> b;
        adj[a].push_back(b);
        adj[b].push_back(a);
    }

    bfs(n);

    if (parent[n] == 0) {
        cout << "IMPOSSIBLE" << endl;
    } else {
        vector<int> path;
        for (int v = n; v != -1; v = parent[v]) {
            path.push_back(v);
        }
        reverse(path.begin(), path.end());

        cout << path.size() << endl;
        for (int v : path) {
            cout << v << " ";
        }
        cout << endl;
    }

    return 0;
}
