# Districts Connection

## [Problem Link](https://codeforces.com/problemset/problem/1433/D)

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
// vector<vi> adj;
// vector<vi> rev;
// vector<bool> vis;

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */

void solve() {
       
    int n;
    cin >> n;
    
    vi a(n);
    
    for(auto &i : a)
        cin >> i;
    
    map<int, int> first;
    map<int, vi> nodes;
    
    for(int i=0; i<n; i++) {
        
        nodes[a[i]].pb(i+1);
        if(first.find(a[i]) == first.end()) {
            first[a[i]] = i+1;
        }
        
    }
    
    vi gangs;
    
    for(auto i : first) {
        gangs.pb(i.first);
    }
    
    if(gangs.size() == 1) {
        cout << "NO" << endl; 
        return;
    }
    
    cout << "YES" << endl;
    
    int last = first[gangs[0]];
    
    for(int i=1; i<gangs.size(); i++) {
        
        for(auto j : nodes[gangs[i]]) {
            cout << last << " " << j << endl;
        }
        
        last = first[gangs[i]];
        
    }
    
    for(auto j : nodes[gangs[0]]) {
        if(j == first[gangs[0]]) {
            continue;
        }
        
        cout << last << " " << j << endl;
    }
    
}

int32_t main() {
    
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    
    int t = 1;
    cin >> t;
    
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
explanation

make separate groups for different gangs
if there's only one gang present,
it's impossible to form such roads
answer exists for all other cases

for simplicity let the gangs be 1 2 3 ... k
choose one member from each gang let it be first[i],
where i is a gang

join all members of gang 2 with first[1],
all members of gang 3 with first[2] and so on
at the end, all membets of gang 1 (except first[1]) with first[k]
*/

// @eclaircp
```
