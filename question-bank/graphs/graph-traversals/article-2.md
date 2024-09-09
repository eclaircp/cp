# Kefka and Park

## [Problem Link](https://codeforces.com/problemset/problem/580/C)

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// data structures

#define int long long
#define ld long double
#define pii pair<int, int>
#define vi vector<int>

// in-built functions

#define pb push_back
#define all(v) v.begin(), v.end()
#define ff first
#define ss second
#define lb lower_bound
#define ub upper_bound
#define endl "\n"

// constants

#define PI 3.1415926535897932384626433832795
#define inf LLONG_MAX
#define null NULL
const int mod = 1e9+7;
// const int mod = 998244353;

// utility functions

int lcm(int a, int b) {
    return (a/__gcd(a, b))*b;
}

int C(int n, int r) {
    
    if(r==0) return 1;
    
    r = min(r, n-r);
    
    int ans = 1;
    
    for(int i=1; i<=r; i++) ans = (ans*(n-i+1))/i;
    
    return ans;    

}

int pow(int x, int n) {
    
    if(n==0) return 1;
    
    int ans = 1;
    
    while(n>0) {
        
        if(n&1) {
            ans *= x;
            n--;
        } else {
            x *= x;
            n = n>>1;
        }
        
    }
    
    return ans;
    
}

// utility classes


// utility storage

// vector<bool> sieve;
// vector<vector<pii>> adj;
// vector<vector<pii>> rev;
// vector<vi> edges;
vector<vi> adj;
// vector<vi> rev;
// vector<bool> vis;
// vi dist;

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */
 
int n, m;
vector<bool> a;
int cnt;

void dfs(int node, int parent, int c) {
    
    int child = 0;
    
    if(c>m) {
        return;
    }
    
    
    for(auto adjNode : adj[node]) {
        if(adjNode != parent) {
            child++;
            if(a[node]) {
                dfs(adjNode, node, c+1);
            } else {
                dfs(adjNode, node, 0);
            }
        }
    }
    
    if(a[node]) {
        c++;
    }
    
    if(child==0 && c<=m) {
        cnt++;
    }
    
}
 
void solve() {
    
    cin >> n >> m;
    a.resize(n+1);
    
    for(int i=1; i<=n; i++) {
        int x;
        cin >> x;
        
        if(x) {
            a[i] = true;
        } else {
            a[i] = false;
        }
    }
    
    adj.resize(n+1);
    
    for(int i=0; i<n-1; i++) {
        int u, v;
        cin >> u >> v;
        
        adj[u].pb(v);
        adj[v].pb(u);
    }
    
    cnt = 0;
    
    dfs(1, -1, 0);
    
    cout << cnt;
    
}

int32_t main() {
    
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    
    int t = 1;
    // cin >> t;
    
    // sieve.resize(200006, true);
    
    // for(int i=2; i*i<=200005; i++) {
    //     if(sieve[i]) {
    //         for(int j=i*i; j<=200005; j+=i) {
    //             sieve[j] = false;
    //         }
    //     }
    // }
    
    while(t--) solve();
    
    return 0;

}

// @eclaircp
```
