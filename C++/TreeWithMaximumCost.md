# Problem link
https://codeforces.com/problemset/problem/1092/F

# Submission ss
![alt text](images/image-2.png)
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


void dfs1(ll node, ll parent, vector<vector<ll>>& adj, vector<ll>& in, vector<ll>& subtree, vector<ll> &a){
    subtree[node] = a[node];
    for(auto& child : adj[node]){
        if(parent == child){
            continue;
        }
        dfs1(child, node, adj, in, subtree, a);
        subtree[node] += subtree[child];
        in[node] += (in[child] + subtree[child]);
    }
}

void dfs2(int n, ll node, ll parent, vector<vector<ll>>& adj, vector<ll>& in, vector<ll>& dp, vector<ll>& subtree, vector<ll>& a){
    for(auto child : adj[node]){
        if(parent == child){
            continue;
        }
        // //Dry Run on a arbitary tree to understand better
        // dp[child] = ((in[child]) + (dp[node] -in[child]) - subtree[child]) + n - subtree[child];
        dp[child] = (subtree[1] - (2LL * subtree[child]) + dp[node]);
        dfs2(n, child, node, adj, in, dp, subtree, a);
    }
}

int main(){
    optimize();
    int n;
    cin >> n;
    vector<ll> a(n + 1, 0);
    for(int i = 1; i <= n; i++){
        cin >> a[i];
    }

    vector<vector<ll>> adj(n + 1);
    for(int i = 0; i < n - 1; i++){
        ll u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // cost(i, v) = For each node (sum of distances of v to i) * weight of ith node 
    vector<ll> in(n + 1, 0); // sum of the distances from the node to all other nodes in in-ward/ downward direction
    vector<ll> dp(n + 1, 0); // sum of the distances from the node to all other nodes
    vector<ll> subtree(n + 1, 0); // Total sum of weights in the subtree of a particular node

    dfs1(1, 0, adj, in, subtree, a);
    dp[1] = in[1];
    dfs2(n, 1, 0, adj, in, dp, subtree, a);
    ll ans = INT_MIN;
    for(int i = 1; i <= n; i++){
        ans = max(ans, dp[i]);
    }
    cout << ans << endl;
    return 0;
}
```

# Explanation or Helpful resourses
For a detailed explanation of the algorithm and to interactively visualize it, please visit the [AlgoVerse Website](https://algooverse.vercel.app/). We encourage you to explore the other algorithm implementations and interactive tools available on the site.

