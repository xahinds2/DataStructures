1. [Next Greater Element I] (https://leetcode.com/problems/next-greater-element-i/)
[GitHub Pages](https://pages.github.com/).

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

2. Next Greater Element II
https://leetcode.com/problems/next-greater-element-ii/

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
