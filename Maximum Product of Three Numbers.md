## Maximum Product of Three Numbers

Given an integer array, find three numbers whose product is maximum and output the maximum product.

<strong>Example 1:</strong>
<pre><code>
<strong>Input:</strong> [1, 2, 3]
<strong>Output:</strong> 6
</code></pre>

<strong>Example 2:</strong>
<pre><code>
<strong>Input:</strong> [1,2,3,4] 
<strong>Output:</strong> 24
</code></pre>

<strong>Note:</strong>

* The length of the given array will be in range [3,104] and all elements are in the range [-1000, 1000].
* Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.

<pre><code>
class Solution {
    public int maximumProduct(int[] nums) {
        Arrays.sort(nums);
        int len = nums.length;
        int res;
        //分情况讨论
        if (nums[len - 1] < 0) {
            res = nums[len - 1] * nums[len - 2] * nums[len - 3];
        } else {//最末尾元素大于零
            //找到乘积为正的最大的两个元素
            int valueofFront = nums[0] * nums[1];
            int valueofEnd = nums[len - 2] * nums[len - 3];
            res = (valueofFront > valueofEnd) ? nums[len - 1] * valueofFront : nums[len - 1] * valueofEnd;
        }
        return res;
    }
}
</code></pre>

***
###<strong><em>分析：</em></strong>
* 该题的解题思路为先对数组进行排序，然后分情况讨论。
* 若排序后的数组的最后一个元素为负，则代表整个数组为负，于是乘积最大的三个数为末尾三个数。
* 若末尾元素为正，则再找到两个乘积为正的最大的元素。此时只需分析开头两个元素和末尾两个元素的乘积孰大孰小即可。

