# Dynamic Programming

1. Minimum Ascii Delete Sum For Two Strings
2. Minimum Cost To Make Two Strings Identical
3. Kadane's Algorithm
4. K Concatenation
5. Maximum Sum Subarray With At Least K Elements
6. Egg Drop
7. Optimal Strategy For A Game
8. Cherry Pickup
9. Probability Of Knight In The Chessboard
10. Highway Billboard
11. Distinct Transformations
12. Numeric Keypad
13. Maximum Difference Of Zeros And Ones In Binary String
14. Maximum Sum Of Two Non-overlapping Subarrays
15. Maximum Sum Of Three Non-overlapping Subarrays
16. Maximum Sum Of M Non-overlapping Subarrays
17. Arithmetic Slices 1
18. Arithmetic Slices 2
19. [Word Break](#word-break)
20. Temple Offerings

# Solutions

### [Word Break](https://leetcode.com/problems/word-break/)
### Recursive with memo :

    public boolean wordBreak(String s, List<String> dict) {
        if(dict.size() == 0 && s.length() == 0) return true;
        return wb(s, dict, 0, new Boolean[s.length()]);
    }
    
    public boolean wb(String s, List<String> dict, int pos, Boolean[] memo){
        if(pos == s.length()) return true;
        if(memo[pos] != null) return memo[pos];
        
        StringBuilder sb = new StringBuilder(s);
        
        for(int i=pos+1; i<=s.length(); i++){
            String sb1 = sb.substring(pos, i);
            
            if(dict.contains(sb1) && wb(s, dict, i, memo)){
                memo[pos] = true;
                return true;
            }
        }
        
        memo[pos] = false;
        return false;
    }

### Tabulation :

    public boolean wordBreak(String s, List<String> dict) {
        if(dict.size() == 0 && s.length() == 0) return true;
        
        boolean[] dp = new boolean[s.length()+1];
        dp[0] = true;
        
        for(int i=1; i <= s.length(); i++){
            for(int j=0; j <= i; j++){
                String str = s.substring(j, i);
                if(dp[j] && dict.contains(str)){
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[s.length()];
    }
