# Stack

1. [Next Greater Element I](#next-greater-element-i)
2. [Next Greater Element II](#next-greater-element-ii)
3. []()
4. []()
5. []()
6. []()
7. []()
8. []()
9. []()
10. []()
11. []()
12. []()



## Next Greater Element I
[Leetcode](https://leetcode.com/problems/next-greater-element-i/)

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

## Next Greater Element II
[Leetcode](https://leetcode.com/problems/next-greater-element-ii/)

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

## Validate Stack Sequences
[Leetcode](https://leetcode.com/problems/validate-stack-sequences/).

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

## Remove Outermost Parentheses
[Leetcode](https://leetcode.com/problems/remove-outermost-parentheses/).

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

## Crawler Log Folder
[Leetcode](https://leetcode.com/problems/crawler-log-folder/).

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

## Design a Stack With Increment Operation
[Leetcode](https://leetcode.com/problems/design-a-stack-with-increment-operation/).

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

## Minimum Add to Make Parentheses Valid
[Leetcode](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/).

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

## Score of Parentheses
[Leetcode](https://leetcode.com/problems/score-of-parentheses/).

class Solution {
    
    public int scoreOfParentheses(String s) {
    
        Stack<Integer> st = new Stack<>();
        st.push(0);
        // storing the levels of bracket in stack
        // for eg in "((()))"
        // levels are 0, 1, 2 for each brackets
        for(char ch : s.toCharArray()){
            
            if(ch == '(') st.push(0);
            else{
                int mul = st.pop();
                int add = st.pop();
                // adding adjacent lvl + current lvl
                // curr lvl = 2 * previous lvl
                // but exception is there for 2*0 == 0
                // for that we are using max function
                st.push(add + Math.max(2*mul, 1));
            }
            // System.out.println(st);
        }
        return st.pop();
    }
}

## Reverse Substrings Between Each Pair of Parentheses
[Leetcode](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/).

class Solution {
    
    public String reverseParentheses(String s) {
        
        int n = s.length();
        
        // making an array which will contain positions of brackets;
        // in (abcd), '(' is in 0 and ')' is in 5 so we will store 5 in 0 and 0 in 5
        int[] pos = new int[n];
        
        // stack will store position for temp
        Stack<Integer> st = new Stack<>();
        
        for(int i=0; i<s.length(); i++){
            char ch = s.charAt(i);
            
            if(ch == '(') st.push(i);
            
            else if(ch == ')'){
                // st.peek() must be the last opening bracket,we need the pos of.
                int j = st.pop();
                // j == pos of opening bracket
                // i == pos of closing bracket
                // lets store this in pos array
                pos[i] = j;
                pos[j] = i;
            }
        }
        // use this to explore the pos array
        // for(int i : pos)
        //     System.out.print(i + " ");
        
        // if we encounter a bracket we will go to its corresponding bracket and will continue to append
        // eg : (abcs), here we ecounter a brack in 0 so we will go to 5 and continue to append
        // till we encounter any bracket, 
        
        StringBuilder sb = new StringBuilder();
        for(int i=0, d=1; i<n; i+=d){
            char ch = s.charAt(i);
            if(ch == '(' || ch == ')'){
                i = pos[i];
                d = -d;
            }
            else sb.append(ch);
        }
        
        return sb.toString();
    }
}

## Minimum Remove to Make Valid Parentheses
[Leetcode](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/).

class Solution {
    
    public String minRemoveToMakeValid(String s) {
        
        List<Integer> useless = new ArrayList<>();
        Stack<Integer> st = new Stack<>();
        
        // storing the index of useless elements
        for(int i=0; i<s.length(); i++){
            char ch = s.charAt(i);
            if(ch == '(') st.push(i);
            else if(ch == ')'){
                if(st.size() > 0 && s.charAt(st.peek()) == '(') st.pop();
                else useless.add(i);
            }
        }
        
        while(!st.isEmpty()) useless.add(st.pop());
        Collections.sort(useless);
        
        // removing the useless elements
        StringBuilder sb = new StringBuilder(s);
        for(int i=useless.size()-1; i>=0; i--){
            sb.deleteCharAt(useless.get(i));
        }
        
        return sb.toString();
    }
}

## Online Stock Span
[Leetcode](https://leetcode.com/problems/online-stock-span/).

class StockSpanner {

    Stack<int[]> stack = new Stack<>();
    
    public int next(int price) {
        int res = 1;
        while (!stack.isEmpty() && stack.peek()[0] <= price)
            res += stack.pop()[1];
        stack.push(new int[]{price, res});
        return res;
    }
}

## Remove K Digits
[Leetcode](https://leetcode.com/problems/remove-k-digits/).

class Solution {

    public String removeKdigits(String num, int k) {
        Stack<Character> st = new Stack<>();
        StringBuilder sb = new StringBuilder();
        
        for(char c : num.toCharArray()){
            while(sb.length()>0 && c < sb.charAt(sb.length()-1) && k>0){
                sb.deleteCharAt(sb.length()-1);
                k--;
            }
            sb.append(c);
        }
        
        while(k > 0){
            sb.deleteCharAt(sb.length()-1);
            k--;
        }
        
        if(sb.length() == 0) sb.append('0');
        
        while(sb.length() > 1 && sb.charAt(0) == '0')
            sb.deleteCharAt(0);

        return sb.toString();
    }
}

## Remove Duplicate Letters
[Leetcode](https://leetcode.com/problems/remove-duplicate-letters/).

class Solution {

    public String removeDuplicateLetters(String s) {
        
        int[] arr = new int[26];
        for(char ch : s.toCharArray()) arr[ch - 'a']++;
        
        boolean[] vis = new boolean[26];
        Stack<Character> st = new Stack<>();
        
        for(char ch : s.toCharArray()){
            int idx = ch-'a';
            arr[idx]--;
            
            if(vis[idx]) continue;
            
            while(!st.isEmpty() && st.peek() > ch && arr[st.peek()-'a'] != 0){
                vis[st.pop()-'a'] = false;
            }
            
            vis[idx] = true;
            st.push(ch);
        }
        
        StringBuilder sb=new StringBuilder();
        while(!st.isEmpty()) sb.append(st.pop());
        
        return sb.reverse().toString();
    }
}
