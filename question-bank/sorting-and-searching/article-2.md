# Scuza

## [Problem Link](https://codeforces.com/problemset/problem/1742/E)

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
     
    int n, q;
    cin >> n >> q;
    
    vi a(n);
    
    for(auto &i : a)
        cin >> i;
    
    vi mx(n);
    
    mx[0] = a[0];
    
    for(int i=1; i<n; i++)
        mx[i] = max(a[i], mx[i-1]);
    
    vi pref(n);
    
    pref[0] = a[0];
    
    for(int i=1; i<n; i++)
        pref[i] = pref[i-1]+a[i];
    
    while(q--) {
        
        int k;
        cin >> k;
        
        int l=0, h=n-1;
        
        while(l<=h) {
            int m = l+(h-l)/2;
            if(k>=mx[m]) {
                l = ++m;
            } else {
                h = --m;
            }
        }
        
        if(h == -1) {
            cout << 0 << " ";
            continue;
        }
        
        cout << pref[h] << " ";
        
    }
    
    cout << endl;
    
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
