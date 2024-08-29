# "redocta".swap(i,i+1)

## [Problem Link](https://atcoder.jp/contests/abc264/tasks/abc264_d)

## Code

```cpp
#include <bits/stdc++.h>

using namespace std;

#define int long long
#define vi vector<int>

// in-built functions

#define pb push_back
#define endl "\n"

/* --------------------------------------------------------------------------------------------------------------------------------- */
/* --------------------------------------------------------------------------------------------------------------------------------- */


void solve() {

    map<char, int> mp;
    string s = "atcoder";

    for(int i=0; i<s.size(); i++)
        mp[s[i]] = i;


    string t;
    cin >> t;

    vi a(s.size());

    int n = a.size();
    
    for(int i=0; i<a.size(); i++) {
        a[i] = mp[t[i]];
    }

    int count = 0;

    for(int i=0; i<n-1; i++) {

        for(int j=0; j<n-i-1; j++) {
            if(a[j]>a[j+1]) {
                swap(a[j], a[j+1]);
                count++;
            }
        }

    }

    cout << count;
}

int32_t main() {

    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    int t = 1;

    while(t--)
        solve();

    return 0;
}
```
