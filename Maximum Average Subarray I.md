## Maximum Average Subarray I

Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.

<strong>Example 1:</strong>
<pre><code>
<strong>Input:</strong> [1,12,-5,-6,50,3], k = 4 
<strong>Output:</strong> 12.75
<strong>Explanation:</strong> Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
</code></pre>

<strong>Note:</strong>

* 1 <= k <= n <= 30,000.
* Elements of the given array will be in the range [-10,000, 10,000].

<pre><code>
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int sum = 0;
        int maxSum = 0;
        for (int i = 0; i < k; i++) {  //设置初始窗口
            sum += nums[i];
        }
        maxSum = sum;
        
        for (int i = k; i < nums.length; i++) {  //挪动窗口，更新最大累加和
            sum = sum - nums[i - k] + nums[i];
            maxSum = Math.max(sum, maxSum);
        }
        return ((double) maxSum) / ((double) k);  //输出最大均值
        
    }
}
</code></pre>

***
* 该题的解题思路为使用滑动窗口，窗口的长度为k。
* 从第k位开始遍历数组，更新最大值即可。