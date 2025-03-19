# codes
#BFS C++

#include<bits/stdc++.h>
using namespace std;

// BFS from given source s
vector<int> bfsOfGraph(vector<vector<int>>& adj, int s)  {
    int V = adj.size();

    // create an array to store the traversal
    vector<int> res;

    // Create a queue for BFS
    queue<int> q;  
    
    // Initially mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Mark source node as visited and enqueue it
    visited[s] = true;
    q.push(s);

    // Iterate over the queue
    while (!q.empty()) {
      
        // Dequeue a vertex from queue and store it
        int curr = q.front();
        q.pop();
        res.push_back(curr);

        // Get all adjacent vertices of the dequeued 
        // vertex curr If an adjacent has not been 
        // visited, mark it visited and enqueue it
        for (int x : adj[curr]) {
            if (!visited[x]) {
                visited[x] = true;
                q.push(x);
            }
        }
    }

    return res;
}

int main()  {

    vector<vector<int>> adj = { {2, 3, 1}, {0},
                                {0, 4}, {0}, {2}};
    int src = 0;
    vector<int> ans = bfsOfGraph(adj, src);
    for(auto i:ans) {
        cout<<i<<" ";
    }
    return 0;
}


#Disconnected

#include<bits/stdc++.h>
using namespace std;

// BFS from given source s
void bfs(vector<vector<int>>& adj, int s, 
        vector<bool>& visited, vector<int> &res) {

    // Create a queue for BFS
    queue<int> q; 

    // Mark source node as visited and enqueue it
    visited[s] = true;
    q.push(s);

    // Iterate over the queue
    while (!q.empty()) {

        // Dequeue a vertex and store it
        int curr = q.front(); 
        q.pop();
        res.push_back(curr);

        // Get all adjacent vertices of the dequeued 
        // vertex curr If an adjacent has not been 
        // visited, mark it visited and enqueue it
        for (int x : adj[curr]) {
            if (!visited[x]) {
                visited[x] = true;
                q.push(x);
            }
        }
    }
}
                      
// Perform BFS for the entire graph which maybe
// disconnected
vector<int> bfsDisconnected(vector<vector<int>>& adj) {
    int V = adj.size();

    // create an array to store the traversal
    vector<int> res;

    // Initially mark all the vertices as not visited
    vector<bool> visited(V, false); 

    // perform BFS for each node
    for (int i = 0; i < adj.size(); ++i) {
        if (!visited[i]) {
            bfs(adj, i, visited, res);
        }
    }

    return res;
}

int main()  {

    vector<vector<int>> adj = { {1, 2}, {0}, {0},
                                {4}, {3, 5}, {4}};
    vector<int> ans = bfsDisconnected(adj);
    for(auto i:ans) {
        cout<<i<<" ";
    }
    return 0;
}


#BFS python

# Function to find BFS of Graph from given source s
def bfsOfGraph(adj, s):
    
    # get number of vertices
    V = len(adj)
    
    # create an array to store the traversal
    res = []
    
    # Create a queue for BFS
    from collections import deque
    q = deque()
    
    # Initially mark all the vertices as not visited
    visited = [False] * V
    
    # Mark source node as visited and enqueue it
    visited[s] = True
    q.append(s)
    
    # Iterate over the queue
    while q:
        
        # Dequeue a vertex from queue and store it
        curr = q.popleft()
        res.append(curr)
        
        # Get all adjacent vertices of the dequeued 
        # vertex curr If an adjacent has not been 
        # visited, mark it visited and enqueue it
        for x in adj[curr]:
            if not visited[x]:
                visited[x] = True
                q.append(x)
                
    return res

if __name__ == "__main__":
    
    # create the adjacency list
    # [ [2, 3, 1], [0], [0, 4], [0], [2] ]
    adj = [ [2, 3, 1], [0], [0, 4], [0], [2] ]
    src = 0
    ans = bfsOfGraph(adj, src)
    for i in ans:
        print(i, end=" ")

#disconnected

# BFS from given source s
from collections import deque

def bfsOfGraph(adj, s, visited, res):
    
    # Create a queue for BFS
    q = deque()
    
    # Mark source node as visited and enqueue it
    visited[s] = True
    q.append(s)
    
    # Iterate over the queue
    while q:
        
        # Dequeue a vertex and store it
        curr = q.popleft()
        res.append(curr)
        
        # Get all adjacent vertices of the dequeued 
        # vertex curr If an adjacent has not been 
        # visited, mark it visited and enqueue it
        for x in adj[curr]:
            if not visited[x]:
                visited[x] = True
                q.append(x)
    return res

# Perform BFS for the entire graph which maybe
# disconnected
def bfsDisconnected(adj):
    V = len(adj)
    
    # create an array to store the traversal
    res = []
    
    # Initially mark all the vertices as not visited
    visited = [False] * V
    
    # perform BFS for each node
    for i in range(V):
        if not visited[i]:
            bfsOfGraph(adj, i, visited, res)
    return res

if __name__ == "__main__":
    adj = [[1, 2], [0], [0],
        [4], [3, 5], [4]]
    ans = bfsDisconnected(adj)
    for i in ans:
        print(i, end=" ")



#dfs C++

#include <bits/stdc++.h>
using namespace std;

// Recursive function for DFS traversal
void DFSRec(vector<vector<int>> &adj, vector<bool> &visited, int s){
  
    visited[s] = true;

    // Print the current vertex
    cout << s << " ";

    // Recursively visit all adjacent vertices
    // that are not visited yet
    for (int i : adj[s])
        if (visited[i] == false)
            DFSRec(adj, visited, i);
}

// Main DFS function that initializes the visited array
// and call DFSRec
void DFS(vector<vector<int>> &adj, int s){
    vector<bool> visited(adj.size(), false);
    DFSRec(adj, visited, s);
}

// To add an edge in an undirected graph
void addEdge(vector<vector<int>> &adj, int s, int t){
    adj[s].push_back(t); 
    adj[t].push_back(s); 
}

int main(){
    int V = 5; 
    vector<vector<int>> adj(V);
  
    // Add edges
    vector<vector<int>> edges={{1, 2},{1, 0},{2, 0},{2, 3},{2, 4}};
    for (auto &e : edges)
        addEdge(adj, e[0], e[1]);

    int s = 1; // Starting vertex for DFS
    cout << "DFS from source: " << s << endl;
    DFS(adj, s); // Perform DFS starting from the source vertex

    return 0;
}
#disconnected'
// C++ program to print DFS
// traversal for a given graph
#include <bits/stdc++.h>
using namespace std;

class Graph {

    // A function used by DFS
    void DFSUtil(int v);

public:
    map<int, bool> visited;
    map<int, list<int> > adj;

    // Function to add an edge to graph
    void addEdge(int v, int w);

    // Prints DFS traversal of the complete graph
    void DFS();
};

void Graph::addEdge(int v, int w)
{
    // Add w to v’s list.
    adj[v].push_back(w);
}

void Graph::DFSUtil(int v)
{
    // Mark the current node as visited and print it
    visited[v] = true;
    cout << v << " ";

    // Recur for all the vertices adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFSUtil(*i);
}

// The function to do DFS traversal. It uses recursive
// DFSUtil()
void Graph::DFS()
{
    // Call the recursive helper function to print DFS
    // traversal starting from all vertices one by one
    for (auto i : adj)
        if (visited[i.first] == false)
            DFSUtil(i.first);
}

// Driver's  Code
int main()
{
    // Create a graph given in the above diagram
    Graph g;
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Following is Depth First Traversal \n";

    // Function call
    g.DFS();

    return 0;
}

#dfs PYTHON

def dfs_rec(adj, visited, s):
    # Mark the current vertex as visited
    visited[s] = True

    # Print the current vertex
    print(s, end=" ")

    # Recursively visit all adjacent vertices
    # that are not visited yet
    for i in adj[s]:
        if not visited[i]:
            dfs_rec(adj, visited, i)


def dfs(adj, s):
    visited = [False] * len(adj)
    # Call the recursive DFS function
    dfs_rec(adj, visited, s)

def add_edge(adj, s, t):
    # Add edge from vertex s to t
    adj[s].append(t)
    # Due to undirected Graph
    adj[t].append(s)
    
if __name__ == "__main__":
    V = 5

    # Create an adjacency list for the graph
    adj = [[] for _ in range(V)]

    # Define the edges of the graph
    edges = [[1, 2], [1, 0], [2, 0], [2, 3], [2, 4]]

    # Populate the adjacency list with edges
    for e in edges:
        add_edge(adj, e[0], e[1])

    source = 1
    print("DFS from source:", source)
    dfs(adj, source)


#disconnected

# Python3 program to print DFS traversal
# for complete graph
from collections import defaultdict


# This class represents a directed graph
# using adjacency list representation
class Graph:

    # Constructor
    def __init__(self):

        # Default dictionary to store graph
        self.graph = defaultdict(list)

    # Function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)

    # A function used by DFS
    def DFSUtil(self, v, visited):

        # Mark the current node as visited and print it
        visited.add(v)
        print(v, end=" ")

        # Recur for all the vertices
        # adjacent to this vertex
        for neighbour in self.graph[v]:
            if neighbour not in visited:
                self.DFSUtil(neighbour, visited)

    # The function to do DFS traversal.
    # It uses recursive DFSUtil
    def DFS(self):

        # Create a set to store all visited vertices
        visited = set()

        # Call the recursive helper function
        # to print DFS traversal starting from all
        # vertices one by one
        for vertex in self.graph:
            if vertex not in visited:
                self.DFSUtil(vertex, visited)


# Driver's code
if __name__ == "__main__":
    print("Following is Depth First Traversal")
    g = Graph()
    g.addEdge(0, 1)
    g.addEdge(0, 2)
    g.addEdge(1, 2)
    g.addEdge(2, 0)
    g.addEdge(2, 3)
    g.addEdge(3, 3)

    # Function call
    g.DFS()




