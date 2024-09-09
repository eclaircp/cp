# The Labyrinth

## [Problem Link](https://codeforces.com/problemset/problem/616/C)

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
 
int n, m;
vector<vector<char>> a;
vector<vector<bool>> vis, vis1;
vector<vector<int>> cnt, type;
int T;

int di[] = {1, 0, -1, 0};
int dj[] = {0, 1, 0, -1};
 
void dfs(int i, int j) {
    
    vis[i][j] = true;
    type[i][j] = T;
    cnt[i][j]++;
    
    for(int k=0; k<4; k++) {
        
        int ni = i+di[k];
        int nj = j+dj[k];
        
        if(ni<0 || ni>=n || nj<0 || nj>=m || vis[ni][nj] || a[ni][nj]=='*') {
            continue;
        }
        
        cnt[ni][nj] = cnt[i][j];
        
        dfs(ni, nj);
        
        cnt[i][j] = max(cnt[i][j], cnt[ni][nj]);
        
    }
    
}

void dfs1(int i, int j) {
    
    vis1[i][j] = true;
    
    for(int k=0; k<4; k++) {
        int ni = i+di[k];
        int nj = j+dj[k];
        
        if(ni>=0 && ni<n && nj>=0 && nj<m && !vis1[ni][nj] && a[ni][nj]=='.') {
            cnt[ni][nj] = max(cnt[i][j], cnt[ni][nj]);
            dfs1(ni, nj);
            cnt[i][j] = max(cnt[i][j], cnt[ni][nj]);
        }
    }
    
}
 
void solve() {
    
    cin >> n >> m;
    a.resize(n, vector<char> (m));
    
    for(auto &i : a) {
        for(auto &j : i) {
            cin >> j;
        }
    }
    
    vis.resize(n, vector<bool> (m, false));
    vis1.resize(n, vector<bool> (m, false));
    cnt.resize(n, vi(m, 0));
    type.resize(n, vi(m));
    
    T = 0;
    
    for(int i=0; i<n; i++) {
        for(int j=0; j<m; j++) {
            if(!vis[i][j] && a[i][j]=='.') {
                T++;
                dfs(i, j);
            }
        }
    }
    
    for(int i=0; i<n; i++) {
        for(int j=0; j<m; j++) {
            if(!vis1[i][j] && a[i][j]=='.') {
                dfs1(i, j);
            }
        }
    }
    
    for(int i=0; i<n; i++) {
        for(int j=0; j<m; j++) {
            if(a[i][j] == '.') {
                cout << '.';
            } else {
                
                set<pair<int, int>> st;
                
                for(int k=0; k<4; k++) {
                    int ni = i+di[k];
                    int nj = j+dj[k];
                    
                    if(ni>=0 && ni<n && nj>=0 && nj<m && a[ni][nj]=='.') {
                        
                        st.insert({type[ni][nj], cnt[ni][nj]});
                        
                    }
                }
                
                int ans = 0;
                
                for(auto i : st) {
                    ans += i.ss;
                }
                
                cout << (ans+1)%10;
                
            }
        }
        
        cout << endl;
    }
    
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
