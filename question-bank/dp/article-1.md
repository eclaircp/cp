# Three Activities

## [Problem Link](https://codeforces.com/problemset/problem/1914/D)

## Code

```cpp
// memoization

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
 
int n;
vector<vi> a, dp;
 
int f(int i, int taken) {
	
	if(i<0) {
		
		if(taken == 7) {
			return 0;
		}
		
		return -1e9;
		
	}
	
	if(dp[i][taken] != -1) {
		return dp[i][taken];
	}
	
	int ans = f(i-1, taken);
	
	for(int j=0; j<3; j++) {
		
		if(taken & (1<<j)) continue;
		
		ans = max(ans, a[i][j] + f(i-1, (taken | (1<<j))));
		
	}
	
	return dp[i][taken] = ans;
	
}
 
void solve() {
	
	cin >> n;
	
	a.resize(n, vi(3));
	dp.resize(n, vi(8, -1));
	
	for(int j=0; j<3; j++) {
		for(int i=0; i<n; i++)
			cin >> a[i][j];
	}
	
	cout << f(n-1, 0) << endl;
	
	a.clear();
	dp.clear();
	 
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

```cpp
// tabulation

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

int n;
vector<vi> a, dp;

void solve() {
	
	cin >> n;
	
	a.resize(n, vi(3));
	dp.resize(n, vi(8, -1));
	
	for(int j=0; j<3; j++) {
		for(int i=0; i<n; i++)
			cin >> a[i][j];
	}

  // dp state
  // dp[i][taken] = max number of people who can be added if taken wale activities will be done in future

	// base case
	dp[0][0] = dp[0][1] = dp[0][2] = dp[0][4] = -1e9;
	dp[0][3] = a[0][2];
	dp[0][5] = a[0][1];
	dp[0][6] = a[0][0];
	dp[0][7] = 0;
	
	
	for(int i=1; i<n; i++) {
		
		for(int taken=0; taken<8; taken++) {
			
			dp[i][taken] = dp[i-1][taken];
			
			for(int j=0; j<3; j++) {
				if(taken & (1<<j)) continue;
				
				dp[i][taken] = max(dp[i][taken], a[i][j] + dp[i-1][(taken | (1<<j))]);
			}
			
		}
		
	}
		
	cout << dp[n-1][0] << endl;
	
	a.clear();
	dp.clear();
	 
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

```cpp
// space optimization

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

int n;
vector<vi> a;
vi dp;

void solve() {
	
	cin >> n;
	
	a.resize(n, vi(3));
	dp.resize(8);
	
	for(int j=0; j<3; j++) {
		for(int i=0; i<n; i++)
			cin >> a[i][j];
	}
	
	// base case
	dp[0] = dp[1] = dp[2] = dp[4] = -1e9;
	dp[3] = a[0][2];
	dp[5] = a[0][1];
	dp[6] = a[0][0];
	dp[7] = 0;
	
	
	for(int i=1; i<n; i++) {
		
		vi temp(8);
		
		for(int taken=0; taken<8; taken++) {
			
			temp[taken] = dp[taken];
			
			for(int j=0; j<3; j++) {
				if(taken & (1<<j)) continue;
				
				temp[taken] = max(temp[taken], a[i][j] + dp[(taken | (1<<j))]);
			}
			
		}
		
		dp = temp;
		
	}
		
	cout << dp[0] << endl;
	
	a.clear();
	dp.clear();
	 
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
