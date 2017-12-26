## Missing Number

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example:</br>
Given nums = [0, 1, 3] return 2.

<pre><code>
class Solution {
    public int missingNumber(int[] nums) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
        }
        
        return ((nums.length + 1) * nums.length / 2) - sum;
    }
}
</code></pre>

* 所缺少元素为累加和减去数组的和。