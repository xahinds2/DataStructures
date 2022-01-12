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
11. [Binary Tree Maximum Path Sum](#binary-tree-maximum-path-sum)
12. [Node to Root Path](#Node-to-Root-Path)
13. [Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)
14. [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
15. [Lowest Common Ancestor of Deepest Leaves](#lowest-common-ancestor-of-deepest-leaves)
16. [Flatten Binary Tree to Linked List](#flatten-binary-tree-to-linked-list)
17. [Cousins in Binary Tree](#cousins-in-binary-tree)
18. [Maximum Difference Between Node and Ancestor](#maximum-difference-between-node-and-ancestor)
19. [All Nodes Distance K in Binary Tree](#all-nodes-distance-k-in-binary-tree)

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

### [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

    int max = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        help(root);
        return max;
    }
    
    public int help(TreeNode root){
        if(root == null) return 0;
        
        int lsum = Math.max(help(root.left), 0);
        int rsum = Math.max(help(root.right), 0);
        max = Math.max(max, root.val + lsum + rsum);
        return root.val + Math.max(lsum, rsum);
    }

### [Node to Root Path](nolink)

    public List<TreeNode> nodeToRootPath(TreeNode root, TreeNode a){
        if(root == null) return new ArrayList<>();
        
        if(root == a){
            List<TreeNode> list = new ArrayList<>();
            list.add(root);
            return list;
        }
        
        List<TreeNode> llist = nodeToRootPath(root.left, a);
        if(llist.size() > 0){
            llist.add(root);
            return llist;
        }
        
        List<TreeNode> rlist = nodeToRootPath(root.right, a);
        if(rlist.size() > 0){
            rlist.add(root);
            return rlist;
        }
        
        return new ArrayList<>();
      }

### [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null) return root;
        
        List<TreeNode> pathp = nodeToRootPath(root, p);
        List<TreeNode> pathq = nodeToRootPath(root, q);
        
        while(pathp.size() < pathq.size()) pathq.remove(0);
        while(pathp.size() > pathq.size()) pathp.remove(0);
        
        for(int i=0; i<pathp.size(); i++)
            if(pathp.get(i) == pathq.get(i))
                return pathp.get(i);
        
        return null;
    }
      
### [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null) return root;
        
        if(p.val < root.val && q.val < root.val) return lowestCommonAncestor(root.left, p, q);
        else if(p.val > root.val && q.val > root.val) return lowestCommonAncestor(root.right, p, q);
        else return root;
    }

### [Lowest Common Ancestor of Deepest Leaves](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/)

    public TreeNode lcaDeepestLeaves(TreeNode root) {
		if(root == null) return root;
        
		int left = depth(root.left);
		int right = depth(root.right);
        
		if(left == right) return root;
		else if(left > right) return lcaDeepestLeaves(root.left);
		else return lcaDeepestLeaves(root.right);
    }
    
    public int depth(TreeNode root){
        if(root == null) return 0;
        return 1 + Math.max(depth(root.left), depth(root.right));
    }

### [Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

    public void flatten(TreeNode root) {
        if(root == null) return;

        Queue<TreeNode> q = new LinkedList<>();
        makeque(root, q);

        root = q.poll();
        root.left = null;
        makelist(root, q);
    }
    
    public void makeque(TreeNode root, Queue<TreeNode> q){
        if(root == null) return;
        q.add(root);
        makeque(root.left, q);
        makeque(root.right, q);
    }
    
    public void makelist(TreeNode root, Queue<TreeNode> q){
        root.right = q.poll();
        root.left = null;
        if(q.size() > 0) makelist(root.right, q);
    }

### [Cousins in Binary Tree](https://leetcode.com/problems/cousins-in-binary-tree/)

    public boolean isCousins(TreeNode root, int x, int y) {
        int[] depths = new int[2];
        int[] parents = new int[2];
        
        find(root, depths, parents, x, y, 0);
        
        if(depths[0] != depths[1]) return false;
        
        if(parents[0] == parents[1]) return false;
        
        return true;
    }
    
    public void find(TreeNode root, int[] depths, int[] parents, int x, int y, int d){
        if(root == null) return;
        
        if(root.right != null){
            if(root.right.val == x) parents[0] = root.val;
            if(root.right.val == y) parents[1] = root.val;
        }
        
        if(root.left != null){
            if(root.left.val == x) parents[0] = root.val;
            if(root.left.val == y) parents[1] = root.val;
        }

        if(root.val == x) depths[0] = d;
        if(root.val == y) depths[1] = d;
        
        find(root.left, depths, parents, x, y, d+1);
        find(root.right, depths, parents, x, y, d+1);
    }
    
### [Maximum Difference Between Node and Ancestor](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/)

    int res = 0;
    public int maxAncestorDiff(TreeNode root) {
        if(root == null) return 0;
        dfs(root, root.val, root.val);
        return res;
    }
    
    public void dfs(TreeNode root, int min, int max){
        if(root == null) return;
        
        min = Math.min(root.val, min);
        max = Math.max(root.val, max);
        
        res = Math.max(res, max-min);
        
        dfs(root.left, min, max);
        dfs(root.right, min, max);
    }

### [All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        Map<TreeNode, Integer> map = new HashMap<>();
        List<Integer> res = new LinkedList<>();
        find(root, target, map);
        dfs(root, target, K, 0, res, map);
        return res;
    }
    
    public int find(TreeNode root, TreeNode target, Map<TreeNode, Integer> map) {
        if (root == null) return -1;
        if (root == target) {
            map.put(root, 0);
            return 0;
        }
        int left = find(root.left, target, map);
        if (left >= 0) {
            map.put(root, left + 1);
            return left + 1;
        }
		int right = find(root.right, target, map);
		if (right >= 0) {
            map.put(root, right + 1);
            return right + 1;
        }
        return -1;
    }
    
    public void dfs(TreeNode root, TreeNode target, int K, int length, List<Integer> res, Map<TreeNode, Integer> map) {
        if (root == null) return;
        if (map.containsKey(root)) length = map.get(root);
        if (length == K) res.add(root.val);
        dfs(root.left, target, K, length + 1, res, map);
        dfs(root.right, target, K, length + 1, res, map);
    }
