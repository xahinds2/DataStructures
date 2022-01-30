# Dynamic Programming

1. [Largest Square Sub-matrix With All 1's](#largest-square-sub-matrix-with-all-ones)
2. [Print All Paths With Minimum Jumps](#Print-All-Paths-With-Minimum-Jumps)
3. [Print All Paths With Minimum Cost](#Print-All-Paths-With-Minimum-Cost)
4. [Print All Paths With Maximum Gold](#Print-All-Paths-With-Maximum-Gold)
5. [Print All Paths With Target Sum Subset](#print-all-paths-with-target-sum-subset)
6. [Print All Results In 0-1 Knapsack](#zero-one-knapsack)
7. [2 Keys Keyboard](#2-keys-keyboard)
8. [Longest Increasing Subsequence](#longest-increasing-subsequence)
9. [Print All Longest Increasing Subsequences](#longest-increasing-subsequence-with-print)
10. [Maximum Sum Increasing Subsequence](#msis)
11. [Longest Bitonic Subsequence](#lbs)
12. [Maximum Non-overlapping Bridges](#max-non-overlapping-bridges)
13. [Russian Doll Envelopes](#max-non-overlapping-bridges) - same logic
14. [Min Squares](#min-squares)
15. Catalan Number
16. Number Of Bsts
17. Count Of Valleys And Mountains
18. Count Brackets
19. Circle And Chords
20. Number Of Ways Of Triangulation

# Solutions

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

### [Print All Paths With Minimum Jumps](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/min-jumps-re-official/ojquestion)

    public static void Solution(int arr[]){
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
        
        System.out.println(dp[0]);
        printpaths(dp, arr, "0", 0);
    }
    
    public static void printpaths(Integer[] dp, int[] arr, String p, int k){
        if(k == dp.length-1) System.out.println(p + " .");
        
        for(int i=1; i<= arr[k] && (i+k) < dp.length; i++){
            int idx = k+i;
            if(dp[idx] != null && dp[idx] == dp[k]-1){
                printpaths(dp, arr, p + " -> " + idx, idx);
            }
        }
    }
    
    // iterate from n-2 to 0 
    // choose the min jump and assign to dp[i]
    // return ith index dp[0]
    
### [Print All Paths With Minimum Cost](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/minimum-cost-path-re-official/ojquestion)

    public static void main(String[] args) throws Exception {
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
        
        for(int i=n-1; i>=0; i--){
            for(int j=m-1; j>=0; j--){
                
                if(i==n-1 && j==m-1) dp[i][j] = arr[i][j];
                else if (i == n-1) dp[i][j] = arr[i][j] + dp[i][j+1];
                else if (j == m-1) dp[i][j] = arr[i][j] + dp[i+1][j];
                else dp[i][j] = arr[i][j] + Math.min(dp[i][j+1], dp[i+1][j]);
            }
        }
        System.out.println(dp[0][0]);
        printpaths(dp, arr, "", 0, 0);
    }
    
    public static void printpaths(int[][] dp, int[][] arr, String p, int m, int n){
        if(m == dp.length-1 && n == dp[0].length-1) System.out.println(p);
        
        if(m+1 < dp.length && n+1 < dp[0].length){
            
            if(dp[m+1][n] < dp[m][n+1]) printpaths(dp, arr, p + "V", m+1, n);
            else if(dp[m+1][n] > dp[m][n+1]) printpaths(dp, arr, p + "H", m, n+1);
            else{
                printpaths(dp, arr, p + "V", m+1, n);
                printpaths(dp, arr, p + "H", m, n+1);
            }
        }
        else if(m+1 < dp.length) printpaths(dp, arr, p + "V", m+1, n);
        else if(n+1 < dp[0].length) printpaths(dp, arr, p + "H", m, n+1);
    }

### [Print All Paths With Maximum Gold](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/goldmine-re-official/ojquestion)

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
            for(int i=n-1; i>=0; i--){
                
                if(j == m-1) dp[i][j] = arr[i][j];
                else if (i == 0) dp[i][j] = arr[i][j] + Math.max(dp[i][j+1], dp[i+1][j+1]);
                else if (i == n-1) dp[i][j] = arr[i][j] + Math.max(dp[i][j+1], dp[i-1][j+1]);
                else dp[i][j] = arr[i][j] + Math.max(Math.max(dp[i][j+1], dp[i-1][j+1]), dp[i+1][j+1]);
            
                if(j == 0) max = Math.max(max, dp[i][j]);
            }
        }
        System.out.println(max);
        
        ArrayDeque<Pair> que = new ArrayDeque<>();
        
        for(int i=0; i<n; i++)
            if(dp[i][0] == max) que.add(new Pair("" + i + " ", i, 0));
            
        while(que.size() > 0){
            Pair rem = que.removeFirst();
            int i = rem.i;
            int j = rem.j;
            
            if(j == m - 1) System.out.println(rem.psf);
            else if(i == 0){
                int g = Math.max(dp[i][j+1], dp[i+1][j+1]);
              
                if(g == dp[i][j+1]) que.add(new Pair(rem.psf + "d2 ",i , j+1));
                if(g == dp[i+1][j+1]) que.add(new Pair(rem.psf + "d3 ", i+1, j+1));
            }
            else if(i == n-1){
                int g = Math.max(dp[i][j+1], dp[i-1][j+1]);
                
                if(dp[i-1][j+1] == g) que.add(new Pair(rem.psf + "d1 ", i-1, j+1));
                if(dp[i][j+1] == g) que.add(new Pair(rem.psf + "d2 ", i, j+1));
                
            }
            else {
                int g = Math.max(dp[i][j+1], Math.max(dp[i-1][j+1], dp[i+1][j+1]));
                
                if(dp[i-1][j+1] == g) que.add(new Pair(rem.psf + "d1 ", i-1, j+1));
                if(dp[i][j+1] == g) que.add(new Pair(rem.psf + "d2 ", i, j+1));
                if(dp[i+1][j+1] == g) que.add(new Pair(rem.psf + "d3 ", i+1, j+1));
            }
        }
    }
    
    // Logic :
    // start from the right side of the wall
    // assign the max value possible in dp array + arr
    // and return the max value in first column

### [Print All Paths With Target Sum Subset](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/print-all-paths-with-target-sum-subset-official/ojquestion)

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) arr[i] = Integer.parseInt(br.readLine());
        int tar = Integer.parseInt(br.readLine());
        
        boolean[][] dp = new boolean[n + 1][tar + 1];
        for (int i = 0; i < dp.length; i++) {
            for (int j = 0; j < dp[0].length; j++) {
                if (i == 0 && j == 0) dp[i][j] = true;
                else if (i == 0) dp[i][j] = false;
                else if (j == 0) dp[i][j] = true;
                else {
                    if(dp[i - 1][j] == true) dp[i][j] = true;
                    else {
                        int val = arr[i - 1];
                        if (j >= val && dp[i-1][j-val]) dp[i][j] = true;
                    }
                }
            }
        }
        
        System.out.println(dp[n][tar]);
        Queue<Pair> q = new ArrayDeque<>();
        q.add(new Pair(n,tar,""));
      
        while (q.size() > 0) {
			Pair rp = q.remove();
			if (rp.i == 0 || rp.j == 0) System.out.println(rp.psf);
			else {
				boolean exc = dp[rp.i - 1][rp.j];
				boolean inc = rp.j - arr[rp.i - 1] >= 0 ? dp[rp.i - 1][rp.j - arr[rp.i - 1]] : false;
				
				if(inc) q.add(new Pair(rp.i - 1, rp.j - arr[rp.i - 1], (rp.i - 1) + " " + rp.psf));
				if(exc) q.add(new Pair(rp.i - 1, rp.j, rp.psf));
			}
		}
    }
        
        // Logic :
        // check if it is already target sum
        // else check if it can make target sum with target-val

### [Zero One Knapsack](https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/zero-one-knapsack-official/ojquestion)

        // write your code here
        
        int[][] dp = new int[n + 1][cap + 1];
        for (int i = 1; i < dp.length; i++) {
            for(int j = 1; j < dp[0].length; j++){
                
                int val = values[i - 1];
                int wt = wts[i - 1];
                
                if(j >= wt) dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - wt] + val);
                else dp[i][j] = dp[i - 1][j];
            }
        }
        System.out.println(dp[n][cap]);
        
        Queue<Pair> q = new ArrayDeque<>();
        q.add(new Pair(n,cap,""));
      
        while (q.size() > 0) {
		Pair rp = q.remove();
		if (rp.i == 0 || rp.j == 0) System.out.println(rp.psf);
		else {
			int w = wts[rp.i - 1];
			int v = values[rp.i - 1];
			    
			int exc = dp[rp.i - 1][rp.j];
			int inc = rp.j - w >= 0 ? (dp[rp.i - 1][rp.j - w] + v) : Integer.MIN_VALUE;
				
			if (dp[rp.i][rp.j] == inc) q.add(new Pair(rp.i - 1, rp.j - w, (rp.i-1) + " " + rp.psf));
			if (dp[rp.i][rp.j] == exc) q.add(new Pair(rp.i - 1, rp.j, rp.psf));
		}
	}
	
	    // Logic :
	    // check for max value
	    // if(j >= w) dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-w] + v);
	    // else dp[i][j] = dp[i-1][j];

### [2 Keys Keyboard](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/2-key-keyboard-official/ojquestion)

	public static int solution(int n) {
		int res = 0;
		for (int d = 2; d <= n; d++) {
			while (n % d == 0) {
				res += d;
				n /= d;
			}
		}
		return res > 0 || n == 1 ? res : n;
	}

### [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        
        int omax = 0;
        for(int i=0; i<n; i++){
            int max = 0;
            
            for(int j=0; j<i; j++)
                if(nums[j] < nums[i]) max = Math.max(max, dp[j]);
            
            dp[i] = max+1;
            omax = Math.max(omax, dp[i]);
        }
        return omax;
    }

### [Longest Increasing Subsequence with print](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lis-re-official/ojquestion)

        for(int i = 0; i < dp.length; i++){
            if(omax == dp[i]){
                queue.add(new Pair(omax, i, arr[i], arr[i] + ""));
            }
        }
	
        while(queue.size() > 0){
            Pair rem = queue.removeFirst();
            
            if(rem.l == 1){
                System.out.println(rem.psf);
            }
            
            for(int j = rem.i - 1; j >= 0; j--){
                if(dp[j] == rem.l - 1 && arr[j] <= rem.v){
                    queue.add(new Pair(dp[j], j, arr[j], arr[j] + " -> " + rem.psf));
                }
            }
        }

### [MSIS](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/msis-official/ojquestion)

    public static void main(String[] args) throws Exception {
        // write your code here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) arr[i] = Integer.parseInt(br.readLine());
        
        int[] dp = new int[n];
        int omax = 0;
        
        for(int i=0; i<n; i++){
            int max = 0;
            
            for(int j=0; j<i; j++){
                if(arr[j] <= arr[i]) max = Math.max(max, dp[j]);
            }
            
            dp[i] = max + arr[i];
            omax = Math.max(dp[i], omax);
        }
        
        System.out.println(omax);
    
    }

### [LBS](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lbs-official/ojquestion)

   public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      int n = Integer.parseInt(br.readLine());
      int[] arr = new int[n];
      for (int i = 0; i < arr.length; i++) {
         arr[i] = Integer.parseInt(br.readLine());
      }
        int[] lis = new int[n];
        
        for(int i=0; i<n; i++){
            int max = 0;
            
            for(int j=0; j<i; j++)
                if(arr[j] < arr[i]) max = Math.max(max, lis[j]);
            
            lis[i] = max+1;
        }
        
        int[] lds = new int[n];
        
        for(int i=n-1; i>=0; i--){
            int max = 0;
            
            for(int j=n-1; j>i; j--)
                if(arr[j] < arr[i]) max = Math.max(max, lds[j]);
            
            lds[i] = max+1;
        }
        
        int omax = 0;
        for(int i=0; i<n; i++){
            omax = Math.max(omax, lis[i] + lds[i] - 1);
        }
        
        System.out.println(omax);
    }

### [Max Non overlapping Bridges](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/max-non-overlapping-bridges-official/ojquestion)

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        Bridge[] brdgs = new Bridge[n];
        
        for (int i = 0; i < brdgs.length; i++) {
            String str = br.readLine();
            brdgs[i] = new Bridge();
            brdgs[i].n = Integer.parseInt(str.split(" ")[0]);
            brdgs[i].s = Integer.parseInt(str.split(" ")[1]);
        }
        
        Arrays.sort(brdgs);
        
        int[] dp = new int[n];
        dp[0] = 1;
        
        int max = 0;
        for(int i=1; i<n; i++){
            int count = 0;
            for(int j=0; j<i; j++){
                if(brdgs[j].s <= brdgs[i].s ) count = Math.max(dp[j], count);
            }
            dp[i] = count+1;
            max = Math.max(dp[i], max);
        }
        
        System.out.println(max);
    }

### [Min Squares](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/min-squares-official/ojquestion)

	public static int solution(int n){
		//write your code here
		
		int[] dp = new int[n+1];
		dp[0] = 0;
		dp[1] = 1;
		
		for(int i=2; i<=n; i++){
		    int min = Integer.MAX_VALUE;
		    for(int j=1; j<=i; j++){
		        int rem = i - j*j;
		        if(rem < 0) break;
		        min = Math.min(dp[rem], min);
		    }
		    dp[i] = min + 1;
		}
		return dp[n];
	}
