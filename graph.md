# Graph

1. [Coloring A Border](coloring-a-border)

# Solutions

### [Coloring A Border](https://leetcode.com/problems/coloring-a-border/)

    public int[][] colorBorder(int[][] grid, int row, int col, int color) {
        int[][] dirs = {{-1,0}, {0,1}, {0,-1}, {1,0}};
        
        // changing every connecte value to negative
        // changing grid[row][col] = - grid[row][col]
        dfs(grid, row, col, dirs);
        
        // now chaning the neg values to the given color
        for(int i=0; i<grid.length; i++)
            for(int j=0; j<grid[0].length; j++)
                if(grid[i][j] < 0) grid[i][j] = color;
        
        return grid;
    }
    
    public void dfs(int[][] grid, int m, int n, int[][] dirs){
        
        int row = grid.length;
        int col = grid[0].length;
        
        int val = grid[m][n];
        grid[m][n] *= -1;
        int count=0;
        
        for(int[] dir : dirs){
            int x = m+dir[0];
            int y = n+dir[1];
            
            if(x >= 0 && y >= 0 && x < row && y < col && Math.abs(grid[x][y]) == val){
                if(grid[x][y] > 0) dfs(grid, x, y, dirs);
                count++;
            }
        }
        
        if(count == 4) grid[m][n] = 0 - grid[m][n];
    }
