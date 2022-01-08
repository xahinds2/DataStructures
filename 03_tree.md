# Tree
1. [Path Sum III](#path-sum-iii)



# Solutions

### [Path Sum III](https://leetcode.com/problems/path-sum-iii/)

    HashMap<Integer,Integer> map = new HashMap<>();
    public int pathSum(TreeNode root, int targetSum) {
        if(root == null) return 0;
        map.put(0, 1);
        return find(root, targetSum, 0);
    }
    
    public int find(TreeNode root, int tar, int sum){
        if(root == null) return 0;
        
        sum += root.val;
        int num = map.getOrDefault(sum-tar, 0);
        map.put(sum, map.getOrDefault(sum, 0)+1);
        int ans = num + find(root.left, tar, sum) + find(root.right, tar, sum);
        map.put(sum, map.get(sum)-1);
        
        return ans;
    }
