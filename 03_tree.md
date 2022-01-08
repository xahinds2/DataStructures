# Tree
1. [Path Sum III](#path-sum-iii)
2. [Binary Tree Right Side View](#binary-tree-right-side-view)


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

### [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

    public List<Integer> rightSideView(TreeNode root) {
    
        if(root == null) return new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        while(q.size() > 0){
            int s = q.size();
            for(int i=0; i<s; i++){
                TreeNode node = q.poll();
                if(i == s-1) list.add(node.val);
                
                if(node.left != null) q.add(node.left);
                if(node.right != null) q.add(node.right);
            }
        }
        return list;
    }
