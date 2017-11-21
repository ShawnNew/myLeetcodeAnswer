### Find the contiguous subarray within an array(containing at least one number) which has the largest sum.


For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

<pre><code>
class Solution {
    public int maxSubArray(int[] nums) {
        int arrayLength = nums.length;
        int sumGlobal = nums[0];
        int sumLocal = nums[0];
        for (int i = 1; i < arrayLength; i++) {
            sumLocal = Math.max(nums[i], nums[i] + sumLocal);
            sumGlobal = Math.max(sumGlobal, sumLocal);
        }
        return sumGlobal;
    }
}
</code></pre>

* 维护两个变量： <code>sumGlobal</code>、<code>sumLocal</code>。其中，<code>sumGlobal</code>表示所有元素的最大值，是最终需要返回的结果。<code>sumLocal</code>表示包含上一个遍历元素的局域最大值。
* 在每个i位置，计算包含上一位元素的最大值加上当前元素之后，最大值是否增大，更新包含i位置的局域最大值。
* 局域最大值和全剧最大值比较，返回最大值到全局最大值。

