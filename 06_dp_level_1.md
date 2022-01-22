# Dynamic Programming

1. [Target Sum Subsets - Dp](#target-sum-subsets-dp)


# Solutions

### [Target Sum Subsets - Dp](https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/target-sum-subsets-dp-official/ojquestion)

        boolean[][] dp = new boolean[m+1][tar+1];
        
        for(int i=0; i<=m; i++)
            for(int j=0; j<=tar; j++)
                if(i == 0 && j == 0) dp[i][j] = true;
                else if(i == 0) dp[i][j] = false;
                else if(j == 0) dp[i][j] = true;
                else
                    if(dp[i-1][j]) dp[i][j] = true;
                    else{
                        int val = arr[i-1];
                        if(j >= val && dp[i-1][j-val]) dp[i][j] = true;
                    }
                    
        System.out.println(dp[m][tar]);
        
        // Logic :
        // check if it is already target sum
        // else check if it can make target sum with target-val
