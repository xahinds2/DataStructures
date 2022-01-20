# Graph - II

## [previous](https://github.com/xahinds2/DataStructures/blob/main/04_graph_I.md)

21. [Mother Vertex](#mother-vertex)
22. [Articulation Point](#articulation-point)
23. [Critical Connection](#critical-connection)
24. [Remove Max Number Of Edges To Keep Graph Fully Traversable](#remove-max-number-of-edges-to-keep-graph-fully-traversable)
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

### [Articulation Point](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/articulation-point-official/ojquestion)

    public static void main(String[] args) {
        
        Scanner scn = new Scanner(System.in);
        int n = scn.nextInt();
        int e = scn.nextInt();
        
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for(int i=0; i<n; i++) graph.add(new ArrayList<>());
        
        for(int i=0; i<e; i++){
            int u = scn.nextInt()-1;
            int v = scn.nextInt()-1;
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        int[] par = new int[n];
        int[] dis = new int[n];
        int[] low = new int[n];
        boolean[] ap = new boolean[n];
        boolean[] vis = new boolean[n];
        par[0] = -1;
        dfs(0, graph, par, dis, low, ap, vis);
        
        int count = 0;
        for(int i=0; i<n; i++){
            if(ap[i] == true) count++;
        }
        System.out.println(count);
    }
    
    public static void dfs(int u, ArrayList<ArrayList<Integer>> graph, int[] par, int[] dis, int[] low, boolean[] ap, boolean[] vis){
        dis[u] = low[u] = time++;
        
        int count = 0;
        vis[u] = true;
        ArrayList<Integer> nbrs = graph.get(u);
        
        for(int i=0; i<nbrs.size(); i++){
            int v = nbrs.get(i);
            
            // mera neighbor hi mera parent ha toh fir choro skip karo
            if(par[u] == v) continue;
            
            // acha thikha parent nhi ha toh check krte ha ki vis ha kya
            // agar visited ha toh fir ye karo
            else if(vis[v] == true) low[u] = Math.min(low[u], dis[v]);
            
            // agar ye nbr unvisited ha toh fir
            // dfs lga k aage jaate rho fir return aane k time
            // low[u] ko relax karo
            else{
                par[v] = u;
                dfs(v, graph, par, dis, low, ap, vis);
                low[u] = Math.min(low[u], low[v]);
                
                if(par[u] == -1){
                    count++;
                    if(count >= 2) ap[u] = true;
                } else {
                    if(low[v] >= dis[u]) ap[u] = true;
                }
            }
        }
    }
    // Logic :
    // mark the articulation point index using par, dis, low array
    // use the comment section in dfs func code to know how
    // count the number of true's

### [Critical Connection](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/critical-connection-official/ojquestion)

    public static void main(String[] args) {
        
        Scanner scn = new Scanner(System.in);
        int n = scn.nextInt();
        int e = scn.nextInt();
        
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for(int i=0; i<n; i++) graph.add(new ArrayList<>());
        
        for(int i=0; i<e; i++){
            int u = scn.nextInt();
            int v = scn.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        int[] par = new int[n];
        int[] dis = new int[n];
        int[] low = new int[n];
        boolean[] ap = new boolean[n];
        boolean[] vis = new boolean[n];
        par[0] = -1;
        List<List<Integer>> ans = new ArrayList<>();
        dfs(0, graph, par, dis, low, ap, vis, ans);
        
        System.out.println(ans);
    }
    
    public static void dfs(int u, ArrayList<ArrayList<Integer>> graph, int[] par, int[] dis, int[] low, boolean[] ap, boolean[] vis, List<List<Integer>> ans){
        dis[u] = low[u] = time++;
        
        int count = 0;
        vis[u] = true;
        ArrayList<Integer> nbrs = graph.get(u);
        
        for(int i=0; i<nbrs.size(); i++){
            int v = nbrs.get(i);
            
            // mera neighbor hi mera parent ha toh fir choro skip karo
            if(par[u] == v) continue;
            
            // acha thikha parent nhi ha toh check krte ha ki vis ha kya
            // agar visited ha toh fir ye karo
            else if(vis[v] == true) low[u] = Math.min(low[u], dis[v]);
            
            // agar ye nbr unvisited ha toh fir
            // dfs lga k aage jaate rho fir return aane k time
            // low[u] ko relax karo
            else{
                par[v] = u;
                dfs(v, graph, par, dis, low, ap, vis, ans);
                low[u] = Math.min(low[u], low[v]);
                
                if(low[v] > dis[u]){
                    List<Integer> temp = new ArrayList<>();
                    temp.add(u);
                    temp.add(v);
                    ans.add(temp);
                }
            }
        }
    }
    // Logic :
    // mark the articulation point index using par, dis, low array
    // use the comment section in dfs func code to know how
    // add the elgible point in lists

### [Remove Max Number Of Edges To Keep Graph Fully Traversable](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/remove-max-number-of-edges-to-keep-graph-fully-traversable-official/ojquestion)

    public int maxNumEdgesToRemove(int n, int[][] edges) {
        Arrays.sort(edges, (a, b) -> Integer.compare(b[0], a[0]));
        
        int[] parenta = new int[n+1];
        int[] parentb = new int[n+1];
        int[] ranka = new int[n+1];
        int[] rankb = new int[n+1];
        
        for(int i=0; i<parenta.length; i++){
            parenta[i] = i;
            parentb[i] = i;
            ranka[i] = 1;
            rankb[i] = 1;
        }
        int mergeda = 1;
        int mergedb = 1;
        int removededge = 0;
        
        for(int[] edge : edges){
            if(edge[0] == 3){
                boolean tempa = union(edge[1], edge[2], parenta, ranka);
                boolean tempb = union(edge[1], edge[2], parentb, rankb);
                if(tempa == true) mergeda++;
                if(tempb == true) mergedb++;
                if(!tempa && !tempb) removededge++;
            } else if(edge[0] == 1){
                boolean tempa = union(edge[1], edge[2], parenta, ranka);
                if(tempa == true) mergeda++;
                else removededge++;
            } else {
                boolean tempb = union(edge[1], edge[2], parentb, rankb);
                if(tempb == true) mergedb++;
                else removededge++;
            }
        }
        
        if(mergeda != n || mergedb != n) return -1;
        
        return removededge;
    }
    // Logic :
    // if a edge does not make cycle use it
    // use union func to merge non cyclic edges
    // sort it to use '3' edge first
