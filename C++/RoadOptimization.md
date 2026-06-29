# Problem link
https://codeforces.com/contest/1625/problem/C

# Submission ss
![alt text](images/image-1.png)
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

const ll INF = 1e18;

int main(){
    optimize();
    int n, l, k;
    cin >> n >> l >> k;
    vector<int> d(n), a(n);
    for(auto& u : d){
        cin >> u;
    }
    d.push_back(l);

    for(auto& u : a){
        cin >> u;
    }

    ll dp[n + 1][k + 1];
    for(int i = 0; i <= k; i++){
        dp[n][i] = 0;
    }

    for(int i = n - 1; i >= 0; i--){
        for(int j = 0; j <= k; j++){
            ll minVal = INF;
            for(int p = 1; p <= j + 1; p++){
                if(i + p > n){
                    break;
                }
                minVal = min(minVal, (dp[i + p][j - (p - 1)] + ((d[i + p] - d[i]) * a[i])));
            }
            dp[i][j] = minVal;
        }
    }
    cout << dp[0][k] << endl;
    
    return 0;
}
```

# Explanation or Helpful resourses
- **Topic**: Road optimization with constraints
- **Reference**: For a detailed explanation of the algorithm and to interactively visualize it, please visit the [AlgoVerse Website](https://algooverse.vercel.app/). We encourage you to explore the other algorithm implementations and interactive tools available on the site.
