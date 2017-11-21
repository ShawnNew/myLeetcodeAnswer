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


### 原始写法：

<pre><code>
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int sum = 0;
        int maxSum = Integer.MIN_VALUE;
        if (nums.length == k) {   //数组的长度等于k时，直接相加
            for (int i = 0; i < k; i++) {
                sum += nums[i];
            }
            maxSum = sum;
        } else {    //数组的长度不等于k时
            for (int i = 0; i < nums.length - k + 1; i++) {   //重新累加k个元素，更新最大maxSum
                sum = 0;
                for (int j = 0; j < k; j++) {
                    sum += nums[i + j];
                }
                maxSum = Math.max(sum, maxSum);
            }
            
        }
        return ((double) maxSum) / ((double) k);  //输出最大均值
        
    }
}
</code></pre>

***
* 原始写法操作数比较多，在对数组遍历的时候，每次都要进行k次加法操作。可以固定窗的大小，在遍历的过程中只是对窗口两端元素进行操作，节省操作数。
* <strong><em>注意在最后返回值的时候的强制类型转换，maxSum和k都要转换成double类型之后再相除。
</em></strong>

***
### 优化写法（每次只操作窗口的两端元素，不用重新累加，节省操作数）：
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