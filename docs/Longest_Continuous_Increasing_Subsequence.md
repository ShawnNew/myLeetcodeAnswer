## Longest Continuous Increasing Subsequence
Given an unsorted array of integers, find the length of longest continuous increasing subsequence.

### Origin Solution
<pre><code>
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int localMaxLen = 1;
        int globalMaxLen = 1;
        
        if (nums.length == 0) {
            globalMaxLen = 0;
        }
        
        for (int i = 1; i < nums.length; i++) {
            
            if (nums[i] <= nums[i - 1]) {
                localMaxLen = 1;
            } 
            if (nums[i] > nums[i - 1]) {
                localMaxLen++;
                globalMaxLen = Math.max(globalMaxLen, localMaxLen); //计数大于最大值，则更新
            }
            
        }
        return globalMaxLen;
    }
}
</code></pre>

***
* 该题的解题思路是在遍历数组的过程中维护两个变量，localMaxLen和globalMaxLen。一个代表当前最大的连续递增数组元素个数，另一个代表返回值。
* 在遍历过程中，满足递增条件的元素localMaxLen++并且一旦超过globalMaxLen则更新返回值。

### 优化代码（简单漂亮）
<pre><code>
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int local = 0,res = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] <= nums[i - 1]) {
                local = 1;
            } else (i = 0 || nums[i] > nums[i - 1]) {
                localMaxLen++;
                res = Math.max(res, local++); //计数大于最大值，则更新
            } 
        }
        return globalMaxLen;
    }
}
</code></pre>