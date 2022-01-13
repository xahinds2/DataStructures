# Graph

1. [Coloring A Border](#coloring-a-border)
2. [Number of Enclaves](#number-of-enclaves)
3. [Number Of Distinct Island](#number-of-distinct-island)
4. [01 Matrix](#01-matrix)
5. [Rotting Oranges](#rotting-oranges)

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
        if (arr == null || arr.length < 1 || arr[0].length < 1)
          return 0;

        HashSet<String> set = new HashSet<String>();

        for (int i = 0; i < arr.length; i++)
          for (int j = 0; j < arr[0].length; j++)
            psf = new StringBuilder();
            if (arr[i][j] == 1) {
              psf.append("o");
              funcall(arr, i, j);
              set.add(psf.toString());
            }

        return set.size();
      }

      private static void funcall(int[][] arr, int i, int j) {

        arr[i][j] = 0;

        if (i + 1 < arr.length && arr[i + 1][j] == 1) { psf.append("d"); funcall(arr, i + 1, j);}
        if (i - 1 >= 0 && arr[i - 1][j] == 1) { psf.append("u"); funcall(arr, i - 1, j); }
        if (j + 1 < arr[0].length && arr[i][j + 1] == 1) { psf.append("r"); funcall(arr, i, j + 1); }
        if (j - 1 >= 0 && arr[i][j - 1] == 1) { psf.append("l"); funcall(arr, i, j - 1); }
        psf.append("b");

      }

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
