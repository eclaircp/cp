# Red and Blue

## [Problem Link](https://codeforces.com/contest/1469/problem/B)

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
// vi dist;

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */
  
void solve() {
    
    int n, m;
    cin >> n;
    
    vi r(n);
    
    for(auto &i : r)
        cin >> i;
        
    cin >> m;
    
    vi b(m);
    
    for(auto &i : b)
        cin >> i;
        
    int s1 = r[0];
    
    int sum = r[0];
    
    for(int i=1; i<n; i++) {
        sum += r[i];
        s1 = max(s1, sum);
    } 
    
    int s2 = b[0];
    
    sum = b[0];
    
    for(int i=1; i<m; i++) {
        sum += b[i];
        s2 = max(s2, sum);
    } 
    
    cout << max({0ll, s1, s2, s1+s2}) << endl;
    
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

// @eclaircp
```
