# Graph - II

## [Graph-II](https://github.com/xahinds2/DataStructures/blob/main/05_graph_II.md)

1.  [Mother Vertex](#mother-vertex)
2.  [Articulation Point](url)
3.  [Critical Connection](url)
4.  [Remove Max Number Of Edges To Keep Graph Fully Traversable](url)
5.  [Number Of Island 2](url)
6.  [Regions Cut By Slashes](url)
7.  [Reconstruct Itinerary](url)
8.  [Rank Transform Of A Matrix](url)
9.  [Accounts Merge](url)
10.  [Minimize Malware Spread](url)
11.  [Minimize Malware Spread 2](url)
12.  [Redundant Connection](url)
13.  [Minimize Hamming Distance After Swap Operations](url)
14.  [Redundant Connection 2](url)
15.  [Satisfiability Of Equality Equation](url)
16.  [Sentence Similarity](url)
17.  [Park Regions Medium](url)
18.  [Kill The Most Monsters](url)
19.  [Number Of Connections To Make Pipeline Connected](url)
20.  [Number Of Provinces](url)

# Solutions

### [Mother Vertex](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/mother-vertex-official/ojquestion)

    public static int findMotherVertex(int n, ArrayList<ArrayList<Integer>> graph){
        
        // step 1 : random dfs and add elements to stack
        boolean[] vis = new boolean[n];
        Stack<Integer> st = new Stack<>();
        for(int i=0; i<n; i++) if(vis[i] == false) dfs1(i, graph, vis, st);
        
        // step 2 : dfs on stack.peek()
        vis = new boolean[n];
        dfs2(st.peek(), graph, vis);
        
        int count = 0;
        for(boolean b : vis) if(!b) count++;
        
        // step 3 : confirmation
        if(count == 0) return st.peek() + 1;
        return -1;
    }
