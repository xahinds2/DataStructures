# Linked List
1. [Middle Of A Linked List](#Middle-Of-A-Linked-List)
2. [Remove Duplicates from Sorted List](#Remove-Duplicates-from-Sorted-List)
3. [Remove Duplicates from Sorted List II](#Remove-Duplicates-from-Sorted-List-II)
4. [Partition List](#Partition-List)


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
