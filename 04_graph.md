# Graph

1. [Coloring A Border](#coloring-a-border)
2. [Number of Enclaves](#number-of-enclaves)
3. [Number Of Distinct Island](#number-of-distinct-island)
4. [01 Matrix](#01-matrix)
5. [Rotting Oranges](#rotting-oranges)
6. [As Far from Land as Possible](#as-far-from-land-as-possible)
7. [Shortest Bridge](#shortest-bridge)
8.  [Bus Routes](#bus-routes)
9.  [Sliding Puzzle Hard](#sliding-puzzle)
10.  [Minimum Number Of Swaps Required To Sort An Array Hard](#minimum-number-of-swaps-required-to-sort-an-array)
11.  [Pepcoder And Reversing Medium](url)
12.  [Course Schedule](#course-schedule-ii)
13.  [Alien Dictionary](#alien-dictionary)
14.  [Kruskal Algorithm](url)
15.  [Optimize Water Distribution](#optimize-water-distribution)
16.  [Swim In Rising Water](#swim-in-rising-water)
17.  [Minimum Cost To Connect All Cities](url)
18.  [Bellman Ford](url)
19.  [Negative Weight Cycle Detection](url)
20.  [Kosaraju Algorithm](url)
21.  [Mother Vertex](url)
22.  [Articulation Point](url)
23.  [Critical Connection](url)
24.  [Remove Max Number Of Edges To Keep Graph Fully Traversable](url)
25.  [Number Of Island 2](url)
26.  [Regions Cut By Slashes](url)
27.  [Reconstruct Itinerary](url)
28.  [Rank Transform Of A Matrix](url)
29.  [Accounts Merge](url)
30.  [Minimize Malware Spread](url)
31.  [Minimize Malware Spread 2](url)
32.  [Redundant Connection](url)
33.  [Minimize Hamming Distance After Swap Operations](url)
34.  [Redundant Connection 2](url)
35.  [Satisfiability Of Equality Equation](url)
36.  [Sentence Similarity](url)
37.  [Park Regions Medium](url)
38.  [Kill The Most Monsters](url)
39.  [Number Of Connections To Make Pipeline Connected](url)
40.  [Number Of Provinces](url)

# Solutions

### [Coloring A Border](https://leetcode.com/problems/coloring-a-border/)

    public int[][] colorBorder(int[][] grid, int row, int col, int color) {
        
        // changing every connecte value to negative
        // changing grid[row][col] = - grid[row][col]
        
        dfs(grid, row, col);
        
        // now chaning the neg values to the given color
        
        for(int i=0; i<grid.length; i++)
            for(int j=0; j<grid[0].length; j++)
                if(grid[i][j] < 0) grid[i][j] = color;
        
        return grid;
    }
    
    public void dfs(int[][] grid, int m, int n){

        int row = grid.length;
        int col = grid[0].length;
        
        int val = grid[m][n];
        grid[m][n] *= -1;
        int count=0;
        
        int[][] dirs = {{-1,0}, {0,1}, {0,-1}, {1,0}};
        
        for(int[] dir : dirs){
            
            int x = m+dir[0];
            int y = n+dir[1];
            
            if(x >= 0 && y >= 0 && x < row && y < col && Math.abs(grid[x][y]) == val){
                if(grid[x][y] > 0) dfs(grid, x, y);
                count++;
            }
        }
        
        if(count == 4) grid[m][n] = 0 - grid[m][n];
    }

### [Number of Enclaves](https://leetcode.com/problems/number-of-enclaves/)

    public int numEnclaves(int[][] grid) {
        
        // calling all the 1's from borders
        for(int i=0; i<grid.length; i++) dfs(grid, i, 0);
        for(int i=0; i<grid.length; i++) dfs(grid, i, grid[0].length-1);
        for(int i=0; i<grid[0].length; i++) dfs(grid, 0, i);
        for(int i=0; i<grid[0].length; i++) dfs(grid, grid.length-1, i);
        
        int count = 0;
        // counting the remaining
        for(int i=0; i<grid.length; i++)
            for(int j=0; j<grid[0].length; j++)
                if(grid[i][j] == 1) count++;
            
        return count;
    }
    
    public void dfs(int[][] grid, int m, int n){
        if(grid[m][n] != 1) return;
        
        int nrow = grid.length;
        int ncol = grid[0].length;
        
        grid[m][n] = -1;
        
        int[][] dirs = {{-1,0},{0,1},{0,-1},{1,0}};
        for(int[] dir : dirs){
            int x = m + dir[0];
            int y = n + dir[1];
            
            if(x >= 0 && y >= 0 && x < nrow && y < ncol)
                dfs(grid, x, y);
        }
    }

### [Number Of Distinct Island](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/number-of-distinct-island-official/ojquestion)

      public static StringBuilder psf = new StringBuilder();

      public static int numDistinctIslands(int[][] arr) {
        if (arr == null || arr.length < 1 || arr[0].length < 1) return 0;

        HashSet<String> set = new HashSet<String>();

        for (int i = 0; i < arr.length; i++)
          for (int j = 0; j < arr[0].length; j++){
            psf = new StringBuilder();
            if (arr[i][j] == 1) {
              psf.append("o");
              funcall(arr, i, j);
              set.add(psf.toString());
            }
          }

        return set.size();
      }

      private static void funcall(int[][] arr, int i, int j) {

        arr[i][j] = 0;

        if (i + 1 < arr.length && arr[i + 1][j] == 1) { psf.append("d"); funcall(arr, i + 1, j); }

        if (i - 1 >= 0 && arr[i - 1][j] == 1) { psf.append("u"); funcall(arr, i - 1, j); }

        if (j + 1 < arr[0].length && arr[i][j + 1] == 1) { psf.append("r"); funcall(arr, i, j + 1); }

        if (j - 1 >= 0 && arr[i][j - 1] == 1) { psf.append("l"); funcall(arr, i, j - 1); }

        psf.append("b");
      }
      
      // Logic
      // we will find '1' using for loop that means we got a island
      // we will use dfs to determine its shape
      // store that shape on a set
      // return the size of the set

### [01 Matrix](https://leetcode.com/problems/01-matrix/)


    public int[][] updateMatrix(int[][] mat) {
        Queue<Pair> q = new LinkedList<>();
        for(int i=0; i<mat.length; i++)
            for(int j=0; j<mat[0].length; j++)
                if(mat[i][j] == 0) q.add(new Pair(i, j));
                else mat[i][j] = -1;

        while(q.size() > 0){
            Pair rem = q.remove();
            dfs(mat, rem.x, rem.y, q);
        }
        
        return mat;
    }
    
    public void dfs(int[][] mat, int i, int j, Queue<Pair> q){
        int nrow = mat.length;
        int ncol = mat[0].length;
        
        int[][] dirs = {{-1,0},{1,0},{0,1},{0,-1}};
        for(int[] dir : dirs){
            int m = i + dir[0];
            int n = j + dir[1];
            if(m >= 0 && n >= 0 && m < nrow && n < ncol && mat[m][n] == -1){
                mat[m][n] = mat[i][j] + 1;
                q.add(new Pair(m, n));
            }
        }
    }
    
    // Logic : 
    // we will change the 1 to -1 and add all th zeros coordinates in q by uing pair class
    // we will travel in the q using whil loop
    // using that if it encounters -1 in the neighbor then we will make it 0 + 1;
    // and also add the index of that -1, and search for its neighbor and mark it 1+1
    // like this we can do it for every elements.

### [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

    public int orangesRotting(int[][] mat) {
        boolean notwos = false;
        Queue<Pair> q = new LinkedList<>();
        
        for(int i=0; i<mat.length; i++)
            for(int j=0; j<mat[0].length; j++)
                if(mat[i][j] == 2){
                    q.add(new Pair(i, j));
                }
        
        if(q.size() == 0 ) notwos = true;
        
        int time = -1;
        while(q.size() > 0){
            int size = q.size();
            for(int i = 0; i< size; i++){
                Pair c = q.remove();
                dfs(mat, c.x, c.y, q);
            }
            time++;
        }
        
        for(int i=0; i<mat.length; i++)
            for(int j=0; j<mat[0].length; j++)
                if(mat[i][j] == 1){
                    return -1;
                }
        
        if(notwos) return 0;
        return time;
        
    }

    public void dfs(int[][] mat, int i, int j, Queue<Pair> q){
        int nrow = mat.length;
        int ncol = mat[0].length;

        int[][] dirs = {{-1,0},{1,0},{0,1},{0,-1}};
        for(int[] dir : dirs){
            int m = i + dir[0];
            int n = j + dir[1];
            if(m >= 0 && n >= 0 && m < nrow && n < ncol && mat[m][n] == 1){
                mat[m][n] = 2;
                q.add(new Pair(m, n));
            }
        }
    }

    // Logic : 
    // we will add all th 2's coordinates in q by uing pair class
    // travel in the q using whil loop
    // using that if it encounters 1 in the neighbor then we will make it 2;
    // and also add the index of that 1, and search for its neighbor and mark it 2.
    // like this we can do it for every elements.

### [As Far from Land as Possible](https://leetcode.com/problems/as-far-from-land-as-possible/)

    public int maxDistance(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        Queue<int[]> queue = new LinkedList<>();
        
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                if (grid[i][j] == 1)
                    queue.offer(new int[] { i, j });
        
        if (queue.size() == 0 || queue.size() == m * n) return -1;
        
        int[][] dirs = { { 0, 1 }, { 0, -1 }, { 1, 0 }, { -1, 0 } };
        
        int max = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int[] point = queue.poll();
                for (int[] dir : dirs) {
                    int x = point[0] + dir[0];
                    int y = point[1] + dir[1];
                    if (x >= 0 && y >= 0 && x < m && y < n && grid[x][y] == 0) {
                        grid[x][y] = 1;
                        queue.offer(new int[] { x, y });
                    }
                }
            }
            max++;
        }
        return max - 1;
    }

### [Shortest Bridge](https://leetcode.com/problems/shortest-bridge/)

    int[][] dirs = new int[][] { { 1, 0 }, { -1, 0 }, { 0, 1 }, { 0, -1 } };
    Queue<int[]> queue = new LinkedList<>();
    int[][] grid;
    int row, col;

    public int shortestBridge(int[][] A) {
        grid = A;
        row = A.length;
        col = A[0].length;
        
        boolean[][] visited = new boolean[row][col];
        boolean found = false;

        for (int i = 0; i < row && !found; i++) {
            for (int j = 0; j < col && !found; j++) {
                if (A[i][j] == 1) {
                    dfs(visited, i, j);
                    found = true;
                }
            }
        }
        
        int step = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            while (size-- > 0) {
                int[] cell = queue.poll();
                for (int[] d : dirs) {
                    int x = cell[0] + d[0];
                    int y = cell[1] + d[1];
                    if (x >= 0 && y >= 0 && x < row && y < col && !visited[x][y]) {
                        if (A[x][y] == 1) return step;
                        
                        queue.offer(new int[] { x, y });
                        visited[x][y] = true;
                    }   
                }
            }
            step++;
        }
        
        return -1;
    }

    private void dfs(boolean[][] visited, int x, int y) {
        if (x < 0 || y < 0 || x >= row || y >= col || visited[x][y] || grid[x][y] == 0) {
            return;
        }
        
        visited[x][y] = true;
        queue.offer(new int[] { x, y });
        
        for (int[] d : dirs) {
            dfs(visited, x + d[0], y + d[1]);
        }
    }
    
    // Logic
    // Using dfs add all the '1' of a island 
    // use bfs to search for '1' of another island 
    // return step on getting

### [Bus Routes](https://leetcode.com/problems/bus-routes/)

    public static int numBusesToDestination(int[][] routes, int S, int T) {

        HashMap<Integer, ArrayList<Integer>> stopmap = new HashMap<>();
        for (int i = 0; i < routes.length; i++) {
            for (int j = 0; j < routes[i].length; j++) {
                int busstop = routes[i][j];
                ArrayList<Integer> busno = stopmap.getOrDefault(busstop, new ArrayList<>());
                busno.add(i);
                stopmap.put(busstop, busno);
            }
        }

        LinkedList<Integer> queue = new LinkedList<>();
        HashSet<Integer> stopvis = new HashSet<>();
        HashSet<Integer> busnovis = new HashSet<>();

        queue.addLast(S);
        stopvis.add(S);
        int level = 0;
        while (queue.size() > 0) {
            int size = queue.size();
            while (size-- > 0) {
                Integer rem = queue.removeFirst();
                if (rem == T) return level;

                ArrayList<Integer> buses = stopmap.get(rem);
                for (int bus : buses) {
                    if (busnovis.contains(bus) == true) continue;

                    int[] arr = routes[bus];
                    for (int stop : arr) {
                        if (stopvis.contains(stop) == true) continue;
                        
                        queue.addLast(stop);
                        stopvis.add(stop);
                    }
                    busnovis.add(bus);
                }
            }
            
            level++;
        }
        
        return -1;
    }
    
    // Logic :
    // map a correspoing list of buses accross all bus stops
    // start travelling from source and check for buses using the map created
    // trvel to all unvisited stops at one level and mark them visited
    // like this keep travelling until destination is reach and return the level

### [Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle/)

    public int slidingPuzzle(int[][] board) {
        
        int[][] dirs = {{1,3},{0,2,4},{1,5},{0,4},{1,3,5},{2,4}};
        String tar = "123450";
        String src = "";
        
        for(int i=0; i<board.length; i++)
            for(int val : board[i]){
                src += val;
            }
        
        HashSet<String> set = new HashSet<>();
        Queue<String> q = new LinkedList<>();
        q.offer(src);
        set.add(src);
        
        int level = 0;
        while(q.size() > 0){
            int size = q.size();
            while(size-- > 0){
                String str = q.poll();
                if(str.equals(tar)) return level;
                int i = str.indexOf('0');
                for(int j : dirs[i]){
                    String s = swap(str, i, j);
                    if(!set.contains(s)){
                        q.offer(s);
                        set.add(s);
                    }
                }
            }
            level++;
        }
        return -1;
    }
    
    public String swap(String str, int i, int j){
        char[] ch = str.toCharArray();
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return new String(ch);
    }
    // Logic 
    // store all the possibilities in a q and check them all
    // convert the input to string for better performance

### [Minimum Number Of Swaps Required To Sort An Array](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/minimum-number-of-swaps-required-to-sort-an-array-official/ojquestion)

      public static int minSwaps(int[] arr1) {
          Pair[] arr = new Pair[arr1.length];
          for(int i=0 ; i<arr1.length; i++){
              arr[i] = new Pair(arr1[i], i);
          }

          Arrays.sort(arr);
          boolean[] vis = new boolean[arr.length];

          int count = 0;
          for(int i=0; i<arr.length; i++){
              if(vis[i] == true || i == arr[i].idx){
                  continue;
              } else {
                  int j = i;
                  int clen = 0;
                  while(vis[j] == false){
                      clen++;
                      vis[j] = true;
                      j = arr[j].idx;
                  }
                  count += (clen-1);
              }
          }
          return count;
      }
      
      // Logic :
      // make a arr of pair datatype which also store the index
      // for eg : [2 3 1] -----> [(2,0), (3,1), (1,2)] 
      // now sort it and loop on it [(1,2), (2,0),(3,1)]
      // we will find that 1 was on 2th index so we will use while loop and detect where it stops
      // 1 was on 2th, so we will check 2 was visited or not and we will go on until we find smthing visited
      // visited means we have encountered a cycle
      // we will implement clen variable on that while loop to check the cycle len
      // add the (clen-1) len to totl count
      // for eg to sort 3 elements we need 2 swaps
      // so to sort a cycle of clen we need clen-1 swaps
      
### [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] arr = new int[numCourses];
        List<List<Integer>> graph = new ArrayList<>();
        initialise(arr, graph, prerequisites);
        
        return dfs(arr, graph);
    }
    
    public void initialise(int[] arr, List<List<Integer>> graph, int[][] data){
        int n = arr.length;
        while(n-- > 0) graph.add(new ArrayList<>());
        for(int[] edge : data){
            arr[edge[0]]++;
            graph.get(edge[1]).add(edge[0]);
        }
    }
    
    public int[] dfs(int[] arr, List<List<Integer>> graph){
        int [] order = new int[arr.length]; 
        Queue<Integer> q = new LinkedList<>();
        
        for(int i=0; i<arr.length; i++)
            if(arr[i] == 0) q.add(i);
        
        int vis = 0;
        while(q.size() > 0){
            int val = q.remove();
            order[vis++] = val;
            for(int nbr : graph.get(val)){
                arr[nbr]--;
                if(arr[nbr] == 0) q.add(nbr);
            }
        }
        
        if(vis == arr.length) return order;
        return new int[0];
    }
    
    // make a ndegree array to store the priority of that course
    // add all the 0 degree indx to que and visit their nbrs using graph
    // decrement the degree of nbrs and keep on adding the nbrs if their ndegree is 0
    // and store the element while removing from que

### [Alien Dictionary](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/alien-dictionary-official/ojquestion)

    public static String alienOrder(String[] words) {
      
        HashMap<Character, List<Character>> map = new HashMap<>();
        HashMap<Character, Integer> degree = new HashMap<>();
        Queue<Character> q = new LinkedList<>();
        HashSet<Character> set = new HashSet<>();
        StringBuilder sb = new StringBuilder();
      
        // initialising degree and map
        // map contains the next elements
        // degree contains the priority
        // degree == 0 means it is independent
        
        for(int i=0; i<words.length-1; i++){
            String s1 = words[i];
            String s2 = words[i+1];
            
            // finding the unequal charcter index
            // for eg in anc and af we will find n & f
            
            int j=0;
            while(s1.charAt(j) == s2.charAt(j)){
                j++;
                if(j >= s1.length() || j >= s2.length()){
                    j = -1;
                    break;
                }
            }
            
            // if not found then just skip
            
            if(j == -1) continue;
            
            // we found ch1 & ch2
            char ch1 = s1.charAt(j);
            char ch2 = s2.charAt(j);
            
            // maping ch1 --> ch2
            
            List<Character> list = map.getOrDefault(ch1, new ArrayList<>());
            list.add(ch2);
            map.put(ch1, list);
            
            // increasing degree of ch2 because it is dependent on ch1
            // degree == 0 means it is independent
            
            int d = degree.getOrDefault(ch2, 0);
            degree.put(ch2, d+1);
            set.add(ch2);
        }
        
        // adding other elements as 0 degree
        // using set for uniquesness
        
        for(String s : words){
            for(char c : s.toCharArray())
                if(!set.contains(c)){
                    set.add(c);
                    int d = degree.getOrDefault(c, 0);
                    degree.put(c, d);
                }
        }
        
        // adding all the 0 degree independent characters in que
        for(char c : degree.keySet()){
            if(degree.get(c) == 0){
                q.offer(c);
                set.add(c);
            }
        }
        
        // use while loop and add its next 0 degree elements
        // use flag to detect if there was >0 degree elements
        // if flag == false return empty string
        
        boolean flag = true;
        while(q.size() > 0){
            char rem = q.poll();
            set.add(rem);
            sb.append(rem);
            for(char next : map.getOrDefault(rem, new ArrayList<>())){
                int d = degree.get(next);
                if(d == 1){
                    flag = false;
                    q.offer(next);
                }
                else degree.put(next, d-1);
            }
        }
        
        if (sb.length() != degree.size() || flag == true) return "";
        return sb.toString();
    }

### [Optimize Water Distribution](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/optimize-water-distribution-official/ojquestion)

      public static int minCostToSupplyWater(int n, int[] wells, int[][] pipes) {
          List<List<Pair>> graph = new ArrayList<>();

          for(int i=0; i<=n; i++) graph.add(new ArrayList<>());

          for(int i=0; i<pipes.length; i++){
              int u = pipes[i][0];
              int v = pipes[i][1];
              int w = pipes[i][2];

              graph.get(u).add(new Pair(v, w));
              graph.get(v).add(new Pair(u, w));
          }

          for(int i=0; i< n; i++){
              graph.get(i+1).add(new Pair(0, wells[i]));
              graph.get(0).add(new Pair(i+1, wells[i]));
          }

          int ans = 0;
          boolean[] vis = new boolean[n+1];
          PriorityQueue<Pair> pq = new PriorityQueue<>();
          pq.add(new Pair(0, 0));

          while(pq.size() > 0){
              Pair rem = pq.remove();
              if(vis[rem.v] == true) continue;

              ans += rem.w;
              vis[rem.v] = true;
              List<Pair> nbrs = graph.get(rem.v);
              for(Pair nbr : nbrs){
                  if(vis[nbr.v] == false){
                      pq.add(nbr);
                  }
              }
          }

          return ans;
      }
      
      // Logic
      // make a graph containing the edges of the pipes and also make a virtual well as index 0;
      // total location will be n+1
      // using priorityqueue add the weight of lowest cost if it is not visited
      // add all of its neighbor to the priorityqueue

### [Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/)

    public int swimInWater(int[][] grid) {
        PriorityQueue<Pair> pq = new PriorityQueue<>();
        pq.add(new Pair(0,0, grid[0][0]));
        int n = grid.length;
        boolean[][] vis = new boolean[n][n];
        
        
        int[][] dirs = {{1,0}, {0,1}, {-1,0}, {0,-1}};
        while(pq.size() > 0){
            Pair rem = pq.remove();
            
            if(rem.x == n-1 && rem.y == n-1) return rem.w;
            
            if(vis[rem.x][rem.y] == true) continue;
            
            vis[rem.x][rem.y] = true;
            
            for(int[] dir : dirs){
                int i = rem.x + dir[0];
                int j = rem.y + dir[1];
                
                if(i < 0 || j < 0 || i >= n || j >= n || vis[i][j] == true) continue;
                
                pq.add(new Pair(i, j, Math.max(rem.w, grid[i][j])));
            }
        }
        return 0;
    }
    
    // Logic :
    // using priority queue we will store all the neihgbors of the point
    // we will travel to the nbr with smallest cost and this will give the min cost
