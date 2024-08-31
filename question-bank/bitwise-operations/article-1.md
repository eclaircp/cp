# Make Almost Equal With Mod

## [Problem Link](https://codeforces.com/problemset/problem/1909/B)

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// data structures

#define int long long
#define vi vector<int>

// in-built functions

#define pb push_back
#define endl "\n"

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */

void solve() {
	
	int n;
	cin >> n;
	
	vi a(n);
	
	int mx = inf;
	
	for(auto &i : a) {
		
		cin >> i;
		
	}
	
	for(int i=0; i<=60; i++) {
		
		int k = (1ll<<i);
		
		set<int> unique;
		
		for(int j=0; j<n; j++) {
			unique.insert(a[j]%k);
		}
		
		if(unique.size()==2) {
			cout << k << endl;
			break;
		}
		
	}
	
	   
}

int32_t main() {
    
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    
    int t = 1;
    cin >> t;
    
    while(t--) solve();
    
    return 0;

}
```
