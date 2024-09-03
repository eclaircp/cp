# Removing Smallest Multiples

## [Problem Link](https://codeforces.com/problemset/problem/1734/C)

## Code
```cpp
#include <bits/stdc++.h>

using namespace std;

#define int long long
#define pii pair<int, int>
#define vi vector<int>

// in-built functions

#define pb push_back
#define lb lower_bound //first element not less than value
#define ub upper_bound //first element greater than value
#define ff first
#define ss second
#define all(v) v.begin(), v.end()
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



/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */


void solve() {

    int n;
    cin >> n;

    string s;
    cin >> s;

    vector<bool> dealthWith(n+1, false);

    for(int i=0; i<n; i++) {
        if(s[i] == '1') {
            dealthWith[i+1] = true;
        }
    }

    int cost = 0;

    for(int i=1; i<=n; i++) {

        if(s[i-1] == '1') continue;

        if(!dealthWith[i]) {

            cost += i;
            dealthWith[i] = true;

            for(int j=2*i; j<=n; j+=i) {
                if(s[j-1] == '1') break;
                if(dealthWith[j]) continue;

                dealthWith[j] = true;
                cost += i;
            }

        } else {

            for(int j=2*i; j<=n; j+=i) {
                if(s[j-1] == '1') break;
                if(dealthWith[j]) continue;

                dealthWith[j] = true;
                cost += i;
            }

        }

    }

    cout << cost << endl;
}

int32_t main() {

    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    int t = 1;
    cin >> t;

    while(t--)
        solve();

    return 0;
}

// @eclaircp
```
