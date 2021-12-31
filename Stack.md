1. [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/).

class Solution {

    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        // finding the next greater element for each elements in nums2 using stack
        Stack<Integer> st = new Stack<>();
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for(int val : nums2){
            while(st.size()>0 && val>st.peek()){
                // if this element is greater than previos element
                // for eg in arr [1, 3, 4, 2]
                // at first we pushed 1 in stack
                // so before puhing 3 we got to know that 3 > 1
                // so lets map it using hashmap
                map.put(st.pop(), val);
            }
            st.push(val);
        }

        for(int i=0; i<nums1.length; i++)
            nums1[i] = map.getOrDefault(nums1[i], -1);

        return nums1;
    }
}

2. [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/).

class Solution {

    public int[] nextGreaterElements(int[] nums) {
    
        HashMap<Integer, Integer> map = new HashMap<>();
        Stack<Integer> stack = new Stack<>();
        
        for (int i=0; i<2*nums.length-1; i++) {
            int idx = i % nums.length;
            while (!stack.empty() && nums[idx] > nums[stack.peek()])
                map.put(stack.pop(), idx);
            
            stack.push(idx);
        }
        
        int[] ans = new int[nums.length];
        for(int i=0; i<nums.length; i++){
            int idx = map.getOrDefault(i, -1);
            if(idx != -1) ans[i] = nums[idx];
            else ans[i] = -1;
        }

        return ans;
    }
}

3. [Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/).

class Solution {

    public boolean validateStackSequences(int[] pushed, int[] popped) {
        int num = pushed.length;
        Stack<Integer> st = new Stack<>();
        
        int j=0;
        for(int x : pushed){
            st.push(x);
            while(st.size() > 0 && st.peek() == popped[j]){
                st.pop();
                j++;
            }
        }
        
        return j == num;
    }
}

4. [Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/).

class Solution {

    public String removeOuterParentheses(String s) {
    
        int size = 0;
        StringBuilder str = new StringBuilder();
        
        for(int i=0; i<s.length(); i++){
            char ch = s.charAt(i);
            if(ch == '('){
                if(size > 0) str.append(ch);
                size++;
            }
            if(ch == ')'){
                if(size > 1) str.append(ch);
                size--;
            }
        }
        return str.toString();
    }
}

5. [Crawler Log Folder](https://leetcode.com/problems/crawler-log-folder/).

class Solution {

    public int minOperations(String[] logs) {
    
        int size = 0;
        for(int i=0; i<logs.length; i++){
            String ch = logs[i];
            
            if(ch.equals("../"))size = Math.max(0, size-1);
            else if(ch.equals("./")){}
            else size++;
        }
        
        return size;
    }
}

6. [Design a Stack With Increment Operation](https://leetcode.com/problems/design-a-stack-with-increment-operation/).

class CustomStack {
    
	int[] stack;
    int size;
    int index;
    
    public CustomStack(int maxSize) {
        stack = new int[maxSize];
        size = maxSize;
        index=0;
    }

    public void push(int x) {
       if (index<size) stack[index++] = x;
    }

    public int pop() {
        if(index == 0) return -1;
        return stack[--index];
    }

    public void increment(int k, int val) {
        if(stack.length == 0) return;
        int max = Math.min(k, stack.length);
        for(int i = 0; i<max; i++)
            stack[i] = stack[i] + val;
    }
    
}

7. [Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/).

class Solution {

    public int minAddToMakeValid(String s) {
        
        Stack<Character> st = new Stack<>();
        // storing only the incomplete paranthese and return the size of stack
        
        for(int i=0; i<s.length(); i++){
            char ch = s.charAt(i);
            
            if(ch == '(') st.push(ch);
            else{
                if(st.size()>0 && st.peek() == '(') st.pop();
                else st.push(ch);
            }
        }
        
        return st.size();
    }
}

8. []().
