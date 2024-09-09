# Journey

## [Problem Link](https://codeforces.com/problemset/problem/839/C)

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
vector<bool> vis;
// vi dist;

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */
 
int n;
vector<double> prob;
double ans;

void dfs(int node, int parent) {
    
    vis[node] = true;
    
    int child = 0;
    
    for(auto adjNode : adj[node]) {
        if(!vis[adjNode]) {
            child++;
        }
    }
    
    if(child == 0) {
        return;
    }
    
    ans += prob[parent];
    
    prob[node] = prob[parent]/child;
    
    for(auto adjNode : adj[node]) {
        
        if(!vis[adjNode]) {
            dfs(adjNode, node);
        }
        
    }
        
}
 
void solve() {
    
    cin >> n;
    
    adj.resize(n+1);
    
    for(int i=0; i<n-1; i++) {        int u, v;
        cin >> u >> v;
        
        adj[u].pb(v);
        adj[v].pb(u);
    }
    
    vis.resize(n+1, false);
    prob.resize(n+1);
    
    prob[0] = 1;
    
    ans = 0;
    
    dfs(1, 0);
    
    cout << setprecision(15);
    
    cout << ans;
    
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

/*
explanation:

E(X) = sum(pixi)
where,
X is an event
E(X) is it's expectation
pi is probability of event i with value xi
so, in this case we multiply the robability of
travelling through an edge with the edge weight

since the edge weights are all 1 so it's same as adding
all the probabilities of traversing though each edge

1
|\
2 3
|\
4 5

for this graph, probabilities are
1-2: 0.5
1-3: 0.5
2-4: 0.25 
2-5: 0.25

(2 ke do children hain toh uspe aane ka prob equally divide
ho jayega uske children mein)

let prob[node] = total sum of probabilities of ging from node to all its eddges
we can call it the expectation for the same too as the edge weights are 1
*/

// @eclaircp
```
