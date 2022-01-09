# Tree
1. [Path Sum III](#path-sum-iii)
2. [Binary Tree Right Side View](#binary-tree-right-side-view)
3. [Maximum Width of Binary Tree](#maximum-width-of-binary-tree)
4. [Binary Tree Tilt](#binary-tree-tilt)
5. [Two Sum IV - Input is a BST](#two-sum-iv-input-is-a-bst)


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

### [Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/)

    public int widthOfBinaryTree(TreeNode root) {
        if(root == null) return 0;

        Queue<Pair> q = new LinkedList<>();
        int maxWidth = 0;
        q.add(new Pair(root, 0));
        
        while(q.size() > 0){
            Pair first = q.peek();
            Pair curr = null;
            int s = q.size();
            while(s-- > 0){
                curr = q.poll();
                TreeNode node = curr.key;
                int idx = curr.idx;
                if(node.left != null) q.offer(new Pair(node.left, 2*idx));
                if(node.right != null) q.offer(new Pair(node.right, 2*idx + 1));
            }
            maxWidth = Math.max(maxWidth, curr.idx - first.idx + 1);
        }
        
        return maxWidth;
    }
    
    public class Pair{
        TreeNode key;
        int idx;
        
        Pair(TreeNode key, int idx){
            this.key = key;
            this.idx = idx;
        }
    }

### [Binary Tree Tilt](https://leetcode.com/problems/binary-tree-tilt/)

    int tilt = 0;
    public int findTilt(TreeNode root) {
        tilt(root);
        return tilt;
    }
    
    public int tilt(TreeNode root){
        if(root == null) return 0;
        int lsum = tilt(root.left);
        int rsum = tilt(root.right);
        tilt += Math.abs(lsum - rsum);
        return root.val + lsum + rsum ;
        
    }

### [Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

    public boolean findTarget(TreeNode root, int k) {
        HashSet<Integer> set = new HashSet<>();
        boolean ans = addtoSet(root, set, k);
        return ans;
    }
    
    public boolean addtoSet(TreeNode root, HashSet<Integer> set, int k){
        if(root == null) return false;
        
        if(set.contains(k - root.val)) return true;
        
        set.add(root.val);
        
        boolean left = addtoSet(root.left, set, k);
        if(left) return left;
        
        boolean right = addtoSet(root.right, set, k);
        return right;
    }
