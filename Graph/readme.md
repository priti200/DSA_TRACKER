# Graph Problems

This folder contains solutions to various problems related to **Graphs**, such as traversals, connected components, shortest paths, and more.

## Problem: Number of Provinces

### Problem Link
[LeetCode Problem: Number of Provinces](https://leetcode.com/problems/number-of-provinces/)

### Problem Description

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `i-th` city and `j-th` city are directly connected, and `isConnected[i][j] = 0` otherwise.

A province is a group of directly or indirectly connected cities, and no other cities outside of the group. Your task is to find the number of provinces.

### Example

**Input**:
isConnected = [[1,1,0], [1,1,0], [0,0,1]]


**Output**: 
2



**Explanation**:
- Cities 1 and 2 are directly connected, forming one province.
- City 3 is disconnected from the rest, forming another province.

### 📝 Pseudocode

```plaintext
function findCircleNum(isConnected):
    initialize visited array of size n as false
    initialize count to 0
    for each city i from 0 to n-1:
        if city i is not visited:
            increment count
            call dfs from city i
    return count

function dfs(city):
    mark city as visited
    for each connected city j:
        if city j is connected and not visited:
            call dfs from city j
```


### 💻 Solution
Here’s the complete C++ solution, designed to explore the graph using Depth-First Search (DFS):

```cpp
class Solution {
public:
    void dfs(int V, int startNode, vector<vector<int>>& adjL, vector<bool>& vis) {
        vis[startNode] = true;  // Mark current node as visited
        
        // Traverse all nodes connected to startNode
        for (int j = 0; j < adjL.size(); j++) {
            // If there's a connection and the node hasn't been visited, perform DFS
            if (adjL[startNode][j] && !vis[j]) {
                dfs(V, j, adjL, vis);
            }
        }
    }

    int findCircleNum(vector<vector<int>>& isConnected) {
        int count = 0;  // To count the number of connected components (provinces)
        int V = isConnected.size();  // Number of cities (nodes)
        vector<bool> vis(V, false);  // Keep track of visited nodes
        
        // Loop through all cities (nodes)
        for (int i = 0; i < V; i++) {
            // If the node hasn't been visited, it is a new province
            if (!vis[i]) {
                count++;  // Increment province count
                dfs(V, i, isConnected, vis);  // Perform DFS from this node
            }
        }
        return count;
    }
};
```

### 🚀 Conclusion
This solution effectively utilizes Depth-First Search (DFS) to traverse the graph and count the number of connected components, allowing us to determine the total number of provinces. Happy coding!

