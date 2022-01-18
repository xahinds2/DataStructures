# Graph - II

## [previous](https://github.com/xahinds2/DataStructures/blob/main/04_graph_I.md)

21. [Mother Vertex](#mother-vertex)
22. Articulation Point
23. Critical Connection
24. Remove Max Number Of Edges To Keep Graph Fully Traversable
25. Number Of Island 2
26. Regions Cut By Slashes
27. Reconstruct Itinerary
28. Rank Transform Of A Matrix
29. Accounts Merge
30. Minimize Malware Spread
31. Minimize Malware Spread 2
32. Redundant Connection
33. Minimize Hamming Distance After Swap Operations
34. Redundant Connection 2
35. Satisfiability Of Equality Equation
36. Sentence Similarity
37. Park Regions
38. Kill The Most Monsters
39. Number Of Connections To Make Pipeline Connected
40. Number Of Provinces

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
