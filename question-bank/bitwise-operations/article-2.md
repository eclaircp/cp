# Chloe and the sequence

## [Problem Link](https://codeforces.com/problemset/problem/743/B)

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// data structures

#define int long long
#define vi vector<int>

#define endl "\n"

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */

int f(int n, int k) {
	
	int mid = (1ll<<(n-1));
	
	if(k==mid) {
		return n;
	}
	
	return f(n-1, k%mid);
	
}

void solve() {
	
	int n, k;
	cin >> n >> k;
	
	cout << f(n, k);
	   
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
```
