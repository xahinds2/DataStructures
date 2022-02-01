# LeetCode

### [Reference Links](#reference-links)

## February Daily Challenges

1. [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)


## Weekly Contest

1. [Weekly Contest 279](https://leetcode.com/contest/weekly-contest-279)
2. [Weekly Contest 280](https://leetcode.com/contest/weekly-contest-280)
3. [Weekly Contest 281](https://leetcode.com/contest/weekly-contest-281)
4. [Weekly Contest 282](https://leetcode.com/contest/weekly-contest-282)

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

## Reference Links

## Data Structure and Algorithm
1. https://leetcode.com/discuss/study-guide/494279/Comprehensive-Data-Structure-and-Algorithm-Study-Guide
2. https://leetcode.com/discuss/study-guide/1178887/Compiling-Important-topics-of-data-structures-and-algorithm-And-Coding-tricks
3. https://leetcode.com/discuss/study-guide/1204393/Algo-List

## STL
1. https://leetcode.com/discuss/study-guide/1327203/C%2B%2B-STL-Guide-or-STL-Operations-and-Time-Complexities
2. https://leetcode.com/discuss/study-guide/1154632/C%2B%2B-STL-powerful-guide-or-Compiled-list-of-popular-STL-operations
3. https://leetcode.com/discuss/study-guide/1387739/C%2B%2B-STL-Guide-or-Online-Coding-Rounds-or-Placements-2021-22
4. https://leetcode.com/discuss/study-guide/1359115/All-C%2B%2B-STL-internal-implementation-oror-last_minute_notes-oror-2021
5. https://leetcode.com/discuss/study-guide/1387739/C%2B%2B-STL-Guide-For-Online-Coding-Rounds

## Binary Search
1. https://leetcode.com/discuss/study-guide/1233854/A-NOOB'S-GUIDE-TO-THE-BINARY-SEARCH-ALGORITHM!!!
2. https://leetcode.com/discuss/study-guide/691825/Binary-Search-for-Beginners-Problems-or-Patterns-or-Sample-solutions
3. https://leetcode.com/discuss/study-guide/786126/Python-Powerful-Ultimate-Binary-Search-Template.-Solved-many-problems

## String
1. https://leetcode.com/discuss/study-guide/1333049/collections-of-string-questions-pattern-for-upcoming-placement-2021

## Tree
1. https://leetcode.com/discuss/study-guide/1337373/tree-question-pattern-2021-placement
2. https://leetcode.com/discuss/study-guide/1212004/Binary-Trees-study-guide
3. https://leetcode.com/discuss/study-guide/1394782/Links-to-selected-LeetCode-questions-on-Trees

## Graph
1. https://leetcode.com/discuss/study-guide/1326900/Graph-algorithms-%2B-problems-to-practice
2. https://leetcode.com/problems/cheapest-flights-within-k-stops/discuss/686774/suggestion-for-beginners-bfs-dijkshtra-dp
3. https://leetcode.com/discuss/study-guide/1072548/A-Beginners-guid-to-BFS-and-DFS
4. https://leetcode.com/discuss/study-guide/655708/Graph-For-Beginners-Problems-or-Pattern-or-Sample-Solutions
5. https://leetcode.com/discuss/study-guide/937307/Iterative-or-Recursive-or-DFS-and-BFS-Tree-Traversal-or-In-Pre-Post-and-LevelOrder-or-Views
6. https://leetcode.com/discuss/study-guide/969327/Graph-Algorithms-One-Place-or-Dijkstra-or-Bellman-Ford-or-Floyd-Warshall-or-Prims-or-Kruskals-or-DSU
7. https://leetcode.com/discuss/study-guide/1059477/A-noob's-guide-to-Dijkstra's-Algorithm
8. https://leetcode.com/discuss/general-discussion/655708/Graph-For-Beginners-Problems-or-Pattern-or-Sample-Solutions
9. https://leetcode.com/discuss/general-discussion/1116359/intro-to-floyds-cycle-detection-algorithm
10. https://leetcode.com/discuss/general-discussion/1078072/introduction-to-topological-sort

## Hashmap
1. https://leetcode.com/discuss/study-guide/1068545/HASH-TABLE-and-MAP-POWERFUL-GUIDE-!!!

## Trie
1. https://leetcode.com/discuss/study-guide/680706/Article-on-Trie.-General-Template-and-List-of-problems.
2. https://leetcode.com/discuss/study-guide/931977/Beginner-friendly-guide-to-Trie-Tutorial-%2B-Practice-Problems
3. https://leetcode.com/discuss/general-discussion/1066206/introduction-to-trie

## Sorting Alogrithm
1. https://leetcode.com/discuss/study-guide/1091763/Must-do-all-required-Sorting-Algorithms%3A-Complete-Guide
2. https://leetcode.com/discuss/general-discussion/1088565/top-k-problems-sort-heap-and-quickselect

## Greedy
1. https://leetcode.com/discuss/study-guide/669996/Greedy-for-Beginners-Problems-or-Sample-solutions

# Dynamic Programming
1. https://leetcode.com/discuss/study-guide/1296872/Think-DP-How-I-approach-DP-problems-(Guide-for-Beginners)
2. https://leetcode.com/discuss/study-guide/662866/DP-for-Beginners-Problems-or-Patterns-or-Sample-Solutions
3. https://leetcode.com/discuss/study-guide/1000929/Solved-all-dynamic-programming-(dp)-problems-in-7-months.
4. https://leetcode.com/discuss/study-guide/1050391/Must-do-Dynamic-programming-Problems-Category-wise
5. https://leetcode.com/discuss/study-guide/458695/Dynamic-Programming-Patterns
6. https://leetcode.com/discuss/study-guide/475924/My-experience-and-notes-for-learning-DP
7. https://leetcode.com/discuss/study-guide/491522/Dynamic-Programming-Questions-Thread
8. https://leetcode.com/discuss/study-guide/651719/How-to-solve-DP-String-Template-and-4-Steps-to-be-followed.
9. https://leetcode.com/discuss/study-guide/1437879/Dynamic-Programming-Patterns
10. https://leetcode.com/problems/house-robber/discuss/156523/From-good-to-great.-How-to-approach-most-of-DP-problems.

## Randomized Problem
1. https://leetcode.com/discuss/study-guide/1334408/play-with-randomized-problems-get-out-fear-2021

## Sliding Window
1. https://leetcode.com/discuss/study-guide/657507/Sliding-Window-for-Beginners-Problems-or-Template-or-Sample-Solutions

## Bit Manipulation
1. https://leetcode.com/discuss/study-guide/1150415/Start-Bit-Manipulation-Here

## Interview
1. https://leetcode.com/discuss/study-guide/698684/Interview-Preparation-for-Beginners-DS-or-Algorithms-or-OS-or-System-Design
2. https://leetcode.com/discuss/study-guide/1098600/topics-which-you-cant-skip-interview-preparation-study-plan-using-leetcode
3. https://leetcode.com/discuss/study-guide/1177039/"Practice-More-Learn-More"-greater-Study-Guide-and-Interview-Preparation-Using-LEETCODE
4. https://leetcode.com/discuss/study-guide/1098600/TOPICS-WHICH-YOU-CAN'T-SKIP-INTERVIEW-PREPARATION-or-STUDY-PLAN-USING-LEETCODE
5. https://leetcode.com/discuss/study-guide/1372500/Do-this-during-your-FAANG-interview-to-ace-it!
6. https://leetcode.com/discuss/study-guide/1389824/One-Stop-OOP-Guide-or-Useful-and-Short-topics-for-interviews-or-Object-Oriented-Programming-(C%2B%2B)
7. https://leetcode.com/discuss/study-guide/1596831/Cleared-Google-L5-India-at-age-of-39-~-40
8. https://leetcode.com/discuss/study-guide/1568859/One-Stop-CN-guide-or-Useful-and-Short-topics-for-interviews-or-Computer-Networks

## Random Tips
1. https://leetcode.com/discuss/study-guide/1151183/TIPS-or-HACKS-WHICH-YOU-CAN'T-IGNORE-AS-A-CODER
2. https://leetcode.com/problems/largest-divisible-subset/discuss/684677/3-steps-c-python-java-dp-pen-paper-diagram
3. https://leetcode.com/discuss/study-guide/1159129/RESUME-BUILDING-or-Things-we-read-but-ignore.
4. https://leetcode.com/discuss/general-discussion/1049269/understanding-how-numbers-are-stored-in-the-computer-using-only-0-and-1
5. https://leetcode.com/discuss/study-guide/448285/List-of-questions-sorted-by-common-patterns.
6. https://leetcode.com/discuss/general-discussion/665604/Important-and-Useful-links-from-all-over-the-LeetCode
7. https://leetcode.com/discuss/study-guide/1371455/Can-you-solve-interval-problems-No-Let's-practice!
8. https://leetcode.com/discuss/study-guide/1389824/One-Stop-OOP-Guide-or-Useful-and-Short-topics-for-interviews-or-Object-Oriented-Programming-(C%2B%2B)
9. https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/900050/Fully-explained-all-buy-and-sell-problems-C%2B%2B-oror-Recursive-oror-Memoization-oror-Minor-difference
10. https://leetcode.com/problems/make-sum-divisible-by-p/discuss/854895/how-to-approach-this-kind-of-problem-mind-map
11. https://leetcode.com/problems/interval-list-intersections/discuss/647482/Python-Two-Pointer-Approach-%2B-Thinking-Process-Diagrams
12. https://leetcode.com/discuss/study-guide/1612475/All-leetcode-discuss-lists-and-my-lists-so-far-topic-wisedifficulty-wise
13. https://leetcode.com/problems/linked-list-random-node/discuss/85659/Brief-explanation-for-Reservoir-Sampling

## Backtracking
1. https://leetcode.com/discuss/study-guide/1405817/Backtracking-algorithm-%2B-problems-to-practice
