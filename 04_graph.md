# Graph

1. [Coloring A Border](#coloring-a-border)
2. [Number of Enclaves](#number-of-enclaves)

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
