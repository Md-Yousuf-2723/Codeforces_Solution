# Problem link
https://codeforces.com/problemset/problem/1151/B

# Submission ss
![alt text](images/image.png)
# Submitted Code

```c++
#include<bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_pbds;

typedef long long ll;
typedef unsigned long long ull;
typedef long double lld;
typedef tree<int, null_type, less<int>, rb_tree_tag, tree_order_statistics_node_update> pbds; // find_by_order, order_of_key
#define optimize() ios_base::sync_with_stdio(0);cin.tie(0);cout.tie(0);
#define endl '\n'

int main(){
    optimize();
    int n, m;
    cin >> n >> m;
    vector<vector<int>> grid(n, vector<int> (m));
    for(auto &u : grid){
        for(auto &v : u){
            cin >> v;
        }
    }
    vector<vector<pair<bool,int>>> dp(n, vector<pair<bool,int>>(1024, {false, - 1}));

    for(int i = 0; i < n; i++){
        for(int x = 0; x < 1024; x++){
            if(i == 0){
                for(int j = 0; j < m; j++){
                    if(grid[0][j] == x){
                        dp[0][x] = {true, j};
                        break;
                    } 
                }
                continue;
            }
            
            for(int j = 0; j < m; j++){
                if(dp[i - 1][x ^ grid[i][j]].first){
                    dp[i][x] = {true, j};
                    break;
                }
            }
        }
    }
    for(int x = 1; x < 1024; x++){
        if(dp[n - 1][x].first){
            vector<int> v(n);
            v[n - 1] = dp[n - 1][x].second;
            int currentXOR = x ^ grid[n - 1][v[n - 1]]; // Removing the xor result from the current xor
            cout << "TAK" << endl;
            for(int i = n - 2; i >= 0; i--){
                v[i] = dp[i][currentXOR].second;
                currentXOR ^= grid[i][v[i]];
            }
            for(auto &u : v){
                // 1-based indexing
                cout << u + 1 << " ";
            }
            cout << endl;
            return 0;
        }
    }
    cout << "NIE" << endl;

    return 0;
}
```

# Explanation or Helpful resourses
- **Topic**: Bitmask DP with answer construction
- **Reference**: For a detailed explanation of the algorithm and to interactively visualize it, please visit the [AlgoVerse Website](https://algooverse.vercel.app/). We encourage you to explore the other algorithm implementations and interactive tools available on the site.
