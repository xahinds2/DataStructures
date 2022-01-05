# Linked List
1. [Middle Of A Linked List](#Middle-Of-A-Linked-List)
2. [Remove Duplicates from Sorted List](#Remove-Duplicates-from-Sorted-List)
3. [Remove Duplicates from Sorted List II](#Remove-Duplicates-from-Sorted-List-II)
4. [Partition List](#Partition-List)
5. [Convert Sorted List to Binary Search Tree](#Convert-Sorted-List-to-Binary-Search-Tree)
6. [Swapping Nodes in a Linked List](#Swapping-Nodes-in-a-Linked-List)
7. [Split Linked List in Parts](#split-linked-list-in-parts)


# Solutions

### [Middle Of A Linked List](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/linked-list/middle-of-a-linked-list/ojquestion)

    public static ListNode midNode(ListNode head) {
    
        if (head == null || head.next == null)
            return head;

        ListNode slow = head;
        ListNode fast = head;

        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }

### [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)
    
    public ListNode deleteDuplicates(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;
        
        while(curr != null){
            prev = curr;
            curr = curr.next;
            while(curr != null && curr.val == prev.val)
                curr = curr.next;
                
            prev.next = curr;
        }

        return head;
    }

### [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

    public ListNode deleteDuplicates(ListNode head) {
        
        if(head == null || head.next == null) return head;
        
        while(head.val == head.next.val){
            ListNode temp = head;
            while(temp != null && temp.val == head.val)
                temp = temp.next;
            head = temp;
            if(head == null || head.next == null) return head;
        }
        
        head.next = deleteDuplicates(head.next);
        
        return head;
    }
}

### [Partition List](https://leetcode.com/problems/partition-list/)

    public ListNode partition(ListNode head, int x) {
        
        ListNode a = new ListNode(0);
        ListNode b = new ListNode(0);
        
        ListNode aHead = a;
        ListNode bHead = b;
        ListNode temp = head;
        
        while(temp != null){
            if(temp.val < x){
                a.next = new ListNode(temp.val);
                a = a.next;
            }
            else{
                b.next = new ListNode(temp.val);
                b = b.next;
            }
            temp = temp.next;
        }
        
        a.next = bHead.next;

        if(aHead.next == null)
            aHead.next = bHead.next; 
        
        return aHead.next;
    }

### [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        if (head.next == null) return new TreeNode(head.val);
        
        // finding mid
        ListNode slow = head, pre = null, fast = head;
        while (fast != null && fast.next != null) {
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // pre = mid.previous
        // cut left sub list here
        pre.next = null;
        
        TreeNode root = new TreeNode(slow.val);
        root.left = sortedListToBST(head);
        root.right = sortedListToBST(slow.next);
        
        return root;
    }

### [Swapping Nodes in a Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/)

    public ListNode swapNodes(ListNode head, int k) {
        ListNode fast = head, slow = head;
        ListNode first = head, second = head;
        
        for(int i=1; i< k; i++) 
            fast = fast.next;
        
        first = fast;
    
        while(fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        
        second = slow;
        
        // swap 
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
        
        return head;
    }

### [Split Linked List in Parts](https://leetcode.com/problems/split-linked-list-in-parts/)

    public ListNode[] splitListToParts(ListNode head, int k) {
        
        int size = 0;
        ListNode temp = head;
        for(temp = head; temp != null; temp = temp.next) size++;
        
        int q = size / k, r = size % k;
        
        ListNode[] arr = new ListNode[k];
        
        ListNode prev = null;
        temp = head;
        
        for(int i=0; i<k; i++){
            if(temp != null) arr[i] = temp;
            
            int need = 0;
            if(r > 0) { need = q + 1; r--;}
            else need = q;
            
            int got = 0;
            while(temp != null){
                if(got == need) {
                    prev.next = null;
                    break;
                }
                got++;
                prev = temp;
                temp = temp.next;
            }
        }
        
        return arr;
    }
