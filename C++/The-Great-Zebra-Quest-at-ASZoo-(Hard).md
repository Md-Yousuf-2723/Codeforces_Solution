# Problem link
https://codeforces.com/gym/105940/problem/C

# Submission ss
![alt text](images/image-3.png)
# Submitted Code

```c++
#include<bits/stdc++.h>
#include<ext/pb_ds/assoc_container.hpp>
#include<ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_pbds;

typedef long long ll;
typedef unsigned long long ull;
typedef long double lld;
typedef tree<int, null_type, less<int>, rb_tree_tag, tree_order_statistics_node_update> pbds; // find_by_order, order_of_key
#define optimize() ios_base::sync_with_stdio(0);cin.tie(0);cout.tie(0);
#define endl '\n'

// Multi-source BFS
void multiSourceBFS(vector<ll>& sources, vector<vector<ll>>& adj, vector<ll>& level, vector<bool>& visited){
    // Placing all the nodes in there level order
    queue<ll> q;
    // pushing all the sources nodes into the queue and marking them as level = 0
    for(auto u : sources){
        q.push(u);
        level[u] = 0;
        visited[u] = true;
    }
    
    // standard BFS
    while(!q.empty()){
        int node = q.front();
        q.pop();
        for(auto e : adj[node]){
            if(!visited[e]){
                visited[e] = true;
                q.push(e);
                level[e] = level[node] + 1;
            }
        }
    }
}

int main(){
    optimize();
    int t;
    cin>>t;
    while(t--){
        ll n , m, k;
        cin >> n >> m >> k;
        vector<vector<ll>> adj(n + 1);
        for(int i = 0; i < m; i++){
            ll u, v;
            cin >> u >> v;
            adj[u].push_back(v);
            adj[v].push_back(u);
        }

        vector<ll> sources(k); // Contains all the source nodes
        for(auto& u : sources){
            cin >> u;
        }
        vector<ll> level(n + 1, -1); // Minimum level of any node from any source nodes
        vector<bool> visited(n + 1, false); // Tracks visited nodes

        multiSourceBFS(sources, adj, level, visited);

        for(int i = 1; i <= n; i++){
            cout << level[i] << " ";
        }
        cout << endl;
    }
    return 0;
}
```

# Explanation or Helpful resourses
For a detailed explanation of the algorithm and to interactively visualize it, please visit the [AlgoVerse Website](https://algooverse.vercel.app/). We encourage you to explore the other algorithm implementations and interactive tools available on the site.

