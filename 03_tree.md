# Tree
1. [Path Sum III](#path-sum-iii)
2. [Binary Tree Right Side View](#binary-tree-right-side-view)
3. [Maximum Width of Binary Tree](#maximum-width-of-binary-tree)
4. [Binary Tree Tilt](#binary-tree-tilt)
5. [Two Sum IV - Input is a BST](#two-sum-iv---input-is-a-bst)
6. [Minimum Absolute Difference in BST](#minimum-absolute-difference-in-bst)
7. [Delete Node in a BST](#delete-node-in-a-bst)
8. [All Elements in Two Binary Search Trees](#all-elements-in-two-binary-search-trees)
9. [Path Sum II](#path-sum-ii)
10. [Sum Root to Leaf Numbers](#sum-root-to-leaf-numbers)


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

### [Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)

    int min = Integer.MAX_VALUE;
    Integer prev = null;
    
    public int getMinimumDifference(TreeNode root) {
        if(root == null) return min;
        
        getMinimumDifference(root.left);
        

        if(prev != null) min = Math.min(min, root.val - prev);
        prev = root.val;
        
        getMinimumDifference(root.right);
        
        return min;
    }

### [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)

    public TreeNode deleteNode(TreeNode root, int key) {
        if(root == null) return root;
        
        if(key < root.val) root.left = deleteNode(root.left, key);
        else if(key > root.val) root.right = deleteNode(root.right, key);
        
        else if(root.val == key){
            
            if(root.left == null) return root.right;
            if(root.right == null) return root.left;
            
            TreeNode min = findleft(root.right);
            TreeNode left = root.left;
            root = root.right;
            min.left = left;
        }
        
        return root;
    }
    
    public TreeNode findleft(TreeNode root){
        while(root.left != null) root = root.left;
        return root;
    }

### [All Elements in Two Binary Search Trees](https://leetcode.com/problems/all-elements-in-two-binary-search-trees/)

    public List<Integer> getAllElements(TreeNode root1, TreeNode root2) {
        
        List<Integer> l1 = new LinkedList<>();
        List<Integer> l2 = new LinkedList<>();
        inorder(root1, l1);
        inorder(root2, l2);
        
        List<Integer> list = new ArrayList<>();
        
        while(l1.size() > 0 && l2.size()>0){
            if(l1.get(0) < l2.get(0)) list.add(l1.remove(0));
            else list.add(l2.remove(0));
        }
        
        while(l1.size() > 0) list.add(l1.remove(0));

        while(l2.size() > 0) list.add(l2.remove(0));

        return list;
    }
    
    public void inorder(TreeNode root, List<Integer> l){
        if(root == null) return;
        
        inorder(root.left, l);
        l.add(root.val);
        inorder(root.right, l);
    }

### [Path Sum II](https://leetcode.com/problems/path-sum-ii/)

    List<List<Integer>> lists = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        if(root == null) return lists;
        help(root, targetSum, new ArrayList<>());
        return lists;
    }
    
    public void help(TreeNode root, int targetSum, List<Integer> list){
        if(root == null) return;
        
        list.add(root.val);
        if(root.left == null && root.right == null && root.val == targetSum)
            lists.add(new ArrayList<>(list));
        
        help(root.left, targetSum-root.val, list);
        help(root.right, targetSum-root.val, list);
        
        list.remove((list.size()-1));
    }

### [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

    int sum;
    public int sumNumbers(TreeNode root) {
        if(root == null) return 0;
        help(root, 0);
        return sum;
    }
    
    public void help(TreeNode root, int psum){
        if(root == null) return;
        
        psum = psum * 10 + root.val;
        if(root.left == null && root.right == null)
            sum += psum;
        
        help(root.left, psum);
        help(root.right, psum);
    }
    
