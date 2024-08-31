# StORage Room

## [Problem Link](https://codeforces.com/problemset/problem/1903/B)

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

void solve() {
	
	int n;
	cin >> n;
	
	vector<vi> m(n, vi(n));
	
	for(int i=0; i<n; i++) {
		for(int j=0; j<n; j++) {
			cin >> m[i][j];
		}
	}
	
	vi a(n, 0);
	
	for(int i=0; i<n; i++) {
		
		for(int bit=0; bit<30; bit++) {
			
			int count = 0;
			
			for(int j=0; j<n; j++) {
				
				if(i==j) continue;
				
				if(m[i][j] & (1<<bit))
					count++;
				
			}
			
			if(count == n-1) {
				a[i] |= (1<<bit);
			}
			
		}
		
	}
	
	for(int i=0; i<n; i++) {
		for(int j=0; j<n; j++) {
			if(i==j) continue;
			
			if((a[i]|a[j]) != m[i][j]) {
				cout << "NO" << endl;
				return;
			}
		}
	}
	
	cout << "YES" << endl;
	
	for(auto i : a)
		cout << i << " ";
	
	cout << endl;
	 
}

/*
for every row i check for all j!=i
if a particulr bit is set
if it's set for all the n-1 elements (a[i] ko chhodke)
toh we assume this bit has come from a[i]
it won't affect our answer even if this bit is common to all other elements too
it will be handled in other iterations
this way we form the array a and then the normal check
*/
 
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
