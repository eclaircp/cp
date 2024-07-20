# Lowest Common Ancestor (LCA)

The brute fore method would be to store the path from both the nodes to the root and then check the common part between both,
the last common node from the root will be the LCA.

The following is the code for the same using binary lifting

```cpp
void dfs(int node, int parentNode, vector<vector<int>> &adj, vector<vector<int>> &parent, int n, vector<int> &level, int l = 0) {
    
    // 2^0 = 1-st parent of node is parentNode
    parent[node][0] = parentNode;
    
    level[node] = l;
    
    // calculate all the other parents
    // since we're calculating the parents which are power of 2, there can be log2(n) parents at max for a node
    
    for(int x=1; x<=log2(n); x++) {
        
        parent[node][x] = parent[parent[node][x-1]][x-1];
        
    }
    
    // now, normal dfs
    
    for(auto adjNode : adj[node]) {
        
        if(adjNode==parentNode)
            continue;
        
        dfs(adjNode, node, adj, parent, n, level, l+1);
        
    }
    
}

int getKthParent(int node, int k, const vector<vector<int>> &parent) {
    
    int count = 0;
    
    while(k) {
          
        if(k&1) {
            node = parent[node][count];
        }
        
        k = (k>>1);
        count++;
        
    }
    
    cout << node << endl;
}

void solution(vector<vector<int>> &adj, int n, int q) {
    
    // precompute the parents
    
    vector<vector<int>> parent(n, vector<int> (log2(n)+1));
    vector<int> level(n+1);
    
    dfs(1, -1, adj, parent, n, level); // assumed nodes starting from 1
    
    while(q--) {
        
        int a, b;
        cin >> a >> b;
        
        // if the nodes are already equal, then just return it
        if(a==b)
            cout << a << endl;
        
        // storing higher level node in a
        if(level[a]>level[b])
            swap(a, b);
        
        // bringing a to the level of b if it's at a higher level
        int k = level[a] - level[b];
        
        b = getKthParent(b, k, parent);
        
        for(int i=log2(n); i>=0; i--) {
            
            // if the current levels of the nodes are such that
            // their parents are equal then move them to their parents
            // which will be in the same level
            if(parent[a][i] != parent[b][i]) {
                a = parent[a][i];
                b = parent[b][i];
            }
            
        }
        
        // at the end of the process the immediate parent of any of the
        // nodes will be the lca
        
        cout << parent[a][0] << endl;
        
    }
    
}
```
