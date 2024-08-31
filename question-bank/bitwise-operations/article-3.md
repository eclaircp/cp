# Friendly Arrays

## (Problem Link)[https://codeforces.com/problemset/problem/1870/B]

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// data structures

#define int long long
#define vi vector<int>

// in-built functions

#define endl "\n"

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */

void solve() {
	
	int n, m;
	cin >> n >> m;
	
	vi a(n), b(m);
	
	for(auto &i : a)
		cin >> i;
		
	for(auto &i : b)
		cin >> i;
		
	int x = 0;
	
	for(int i=0; i<m; i++) {
		x = (x | b[i]);
	}
	
	int one = 0;
	int two = 0;
	
	for(int i=0; i<n; i++) {
		
		one = (one ^ a[i]);
		two = (two ^ (a[i] | x));
		
	}
	
	if(n&1) {
		
		cout << one << " " << two << endl;
		
	} else {
		
		cout << two << " " << one << endl;
		
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
