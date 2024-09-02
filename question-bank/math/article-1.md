# Same Parity Summands

## (Problem Link)[https://codeforces.com/problemset/problem/1352/B]

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
       
    int n, k;
    cin >> n >> k;
    
    // saare even
    if((2*k)%2 == n%2) {
        
        if(n-2*k>=0) {
            
            cout << "YES" << endl;
            
            for(int i=0; i<k-1; i++) {
                cout << 2 << " ";
            }
            
            cout << n-2*k+2 << endl;
            
            return;
            
        }
        
    }
    
    // saare odd
    if(n-k>=0 && (n-k)%2==0) {
        
        cout << "YES" << endl;
        
        for(int i=0; i<k-1; i++)
            cout << 1 << " ";
        
        cout << (n-k+1) << endl;
        
        return;
    }
    
    cout << "NO" << endl;
    
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

if all even possible
a1 a2 a3 a4 ... an (all even)
sab mein se kuchh even nikalke an mein add kar denge
taaki saare 2 ban jaye aur an jo bhi bane, even bane



if all odd possible
a1 a2 a3 a4 ... an (all odd)
sab mein se kuchh even nikalke an mein add kar denge
taaki saare 1 ban jaye aur an jo bhi bane, odd bane



if both of these cases are not possible toh it's not possible
to create such an array
*/

// @eclaircp
```
