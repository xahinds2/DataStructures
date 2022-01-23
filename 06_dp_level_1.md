# Dynamic Programming

1. [Target Sum Subsets](#target-sum-subsets)
2. [Zero One Knapsack](#zero-one-knapsack)
3. [Jump Game II](#jump-game-ii)
4. [Goldmine](#goldmine)
5. [Largest Square Sub-matrix With All 1's](#largest-square-sub-matrix-with-all-ones)
6. Print All Paths With Minimum Jumps
7. Print All Paths With Minimum Cost
8. Print All Paths With Maximum Gold
9. Print All Paths With Target Sum Subset
10. Print All Results In 0-1 Knapsack
11. Key Keyboard Medium



# Solutions

### [Target Sum Subsets](https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/target-sum-subsets-dp-official/ojquestion)

    public static void main(String[] args) throws Exception {
        // write your code here
        Scanner scn = new Scanner(System.in);
        
        int m = scn.nextInt();
        
        int[] arr = new int[m];
        for(int i=0; i<m; i++) arr[i] = scn.nextInt();
        
        int tar = scn.nextInt();
        
        boolean[][] dp = new boolean[m+1][tar+1];
        
        for(int i=0; i<=m; i++){
            for(int j=0; j<=tar; j++){
                if(i == 0 && j == 0) dp[i][j] = true;
                else if(i == 0) dp[i][j] = false;
                else if(j == 0) dp[i][j] = true;
                else{
                    if(dp[i-1][j]) dp[i][j] = true;
                    else{
                        int val = arr[i-1];
                        if(j >= val && dp[i-1][j-val]) dp[i][j] = true;
                    }
                }
            }
        }
        
        System.out.println(dp[m][tar]);
    }
        
        // Logic :
        // check if it is already target sum
        // else check if it can make target sum with target-val

### [Zero One Knapsack](https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/zero-one-knapsack-official/ojquestion)

    public static void main(String[] args) throws Exception {
        // write your code here
        Scanner scn = new Scanner(System.in);
        
        int m = scn.nextInt();
        
        int[] arrv = new int[m];
        for(int i=0; i<m; i++) arrv[i] = scn.nextInt();
        
        int[] arrw = new int[m];
        for(int i=0; i<m; i++) arrw[i] = scn.nextInt();
        
        int tar = scn.nextInt();
        
        int[][] dp = new int[m+1][tar+1];
        
        for(int i=1; i<=m; i++){
            for(int j=1; j<=tar; j++){
                int v = arrv[i-1];
                int w = arrw[i-1];
                
                if(j >= w) dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-w] + v);
                else dp[i][j] = dp[i-1][j];
            }
        }
        
        System.out.println(dp[m][tar]);
    }
    // Logic :
    // check for max value
    // if(j >= w) dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-w] + v);
    // else dp[i][j] = dp[i-1][j];

### [Jump Game II](https://leetcode.com/problems/jump-game-ii/)

    public int jump(int[] arr) {
        int n = arr.length;
        
        Integer[] dp = new Integer[n];
        dp[n-1] = 0;
        
        for (int i = n - 2; i >= 0; i--) {
            if (arr[i] > 0) {
                int min = Integer.MAX_VALUE;
                for (int j = 1; j <= arr[i] && i + j < dp.length; j++)
                   if(dp[i + j] != null) min = Math.min(min, dp[i + j]);
                   
                if(min != Integer.MAX_VALUE) dp[i] = min + 1;
            }
        }
        return dp[0];
    }
    
    // iterate from n-2 to 0 
    // choose the min jump and assign to dp[i]
    // return ith index dp[0]

### [Goldmine](https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/goldmine-official/ojquestion)

    public static void main(String[] args) throws Exception {
        // write your code here
        Scanner scn = new Scanner(System.in);
        
        int n = scn.nextInt();
        int m = scn.nextInt();
        
        int[][] arr = new int[n][m];
        
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                arr[i][j] = scn.nextInt();
            }
        }
        
        int[][] dp = new int[n][m];
        int max = Integer.MIN_VALUE;
        for(int j=m-1; j>=0; j--){
            for(int i=0; i<n; i++){
                if(j == m-1) dp[i][j] = arr[i][j];
                else if (i == 0) dp[i][j] = arr[i][j] + Math.max(dp[i][j+1], dp[i+1][j+1]);
                else if (i == n-1) dp[i][j] = arr[i][j] + Math.max(dp[i][j+1], dp[i-1][j+1]);
                else dp[i][j] = arr[i][j] + Math.max(Math.max(dp[i][j+1], dp[i-1][j+1]), dp[i+1][j+1]);
            
                if(j == 0) max = Math.max(max, dp[i][j]);
            }
        }
        System.out.println(max);
    }
    
    // Logic :
    // start from the right side of the wall
    // assign the max value possible in dp array + arr
    // and return the max value in first column

### [Largest Square Sub-matrix With All ones](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/largest-square-sub-matrix-with-all-ones-official/ojquestion)

	public static int solution(int[][] arr) {
		//write your code here
		int n = arr.length;
		int m = arr[0].length;
		
		int[][] dp = new int[n][m];
		int max = 0;
		for(int i=n-1; i>=0; i--){
		    for(int j=m-1; j>=0; j--){
		        if(i == n-1 || j == m-1 || arr[i][j] == 0) dp[i][j] = arr[i][j];
		        else{
		            dp[i][j] = Math.min(dp[i+1][j], Math.min(dp[i+1][j+1], dp[i][j+1])) + 1;
		        }
		        max = Math.max(dp[i][j], max);
		    }
		}
		return max;
	}
	// Logic :
	// start from bottom right
	// if(i == n-1 || j == m-1 || arr[i][j] == 0) dp[i][j] = arr[i][j];
	// else take the min of right, down, right-down and add 1 to it
