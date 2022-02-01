# LeetCode
## February Daily Challenges

1. [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)

## Solutions

### [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

    public int maxProfit(int[] prices) {
        
        int buy = prices[0];
        int profit = 0;
        
        for(int i=1; i<prices.length; i++){
            if(prices[i] < buy) buy = prices[i];
            if(prices[i] - buy > profit) profit = prices[i] - buy;
        }
        
        return profit;
    }

## Weekly Contest

1. [Weekly Contest 279](https://leetcode.com/contest/weekly-contest-279)
2. [Weekly Contest 280](https://leetcode.com/contest/weekly-contest-280)
3. [Weekly Contest 281](https://leetcode.com/contest/weekly-contest-281)
4. [Weekly Contest 282](https://leetcode.com/contest/weekly-contest-282)


## Solutions
