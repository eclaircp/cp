# Binary Lifting

To find k-th parent of a node in a tree, the brute force method would be to do a bfs/dfs traversal and store the parent of each parent.
Then we can run a loop k-times to get the k-th parent of a given node as follows:

```cpp
int getKthParent(int node, int k, int parent[]) {
    
    while(k--) {
        node = parent[node];
    }
    
    return node;
    
}
```

TC: O(n+k) // O(n) for the bfs/dfs and O(k) for finding the k-th parent  
SC: O(n) // to store the n parents

What if we were given q queries with a node and a k each?  
TC using the above method: O(n + qk)

Instead, we'll store the k-th parents such that k is a power of 2.

Then let's say the 2^(x-1)-th parent of node is node1 and 2^(x-1)-th parent of node1 is node2, i.e.,
parent[node][x-1] = node1 and parent[node1][x-1] = node2 then,
2^x-th parent of node is node2, i.e.,

parent[node][x] = node2, which can be derived as,  
   parent[node][x] = parent[node1][x-1]  
=> parent[node][x] = parent[parent[node][x-1]][x-1]

So, if we know parent[node][0], then all the others can be calculated.

```cpp
void dfs(int node, int parentNode, vector<vector<int>> &adj, vector<vector<int>> &parent, int n) {
    
    // 2^0 = 1-st parent of node is parentNode
    parent[node][0] = parentNode;
    
    // calculate all the other parents
    // since we're calculating the parents which are power of 2, there can be log2(n) parents at max for a node
    
    for(int x=1; x<=log2(n); x++) {
        
        parent[node][x] = parent[parent[node][x-1]][x-1];
        
    }
    
    // now, normal dfs
    
    for(auto adjNode : adj[node]) {
        
        if(adjNode==parentNode)
            continue;
        
        dfs(adjNode, node, adj, parent, n);
        
    }
    
}
```

The follwing code snippet shows how the queries are handled:

```cpp
void solution(vector<vector<int>> &adj, int n, int q) {
    
    // precompute the parents
    
    vector<vector<int>> parent(n, vector<int> (log2(n)+1));
    
    dfs(1, -1, adj, parent, n); // assumed nodes starting from 1
    
    while(q--) {
        
        int node, k;
        cin >> node >> k;
        
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
    
}
```

Overall TC: O(nlogn + qlogk)  
Overall SC: O(nlogn)
