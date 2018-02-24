## Shortest Unsorted Continuous Subarray

Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the shortest such subarray and output its length.

#### Example 1：
<pre><code>
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
</code></pre>



#### Note:
	1. Then length of the input array is in range [1, 10,000].
	2. The input array may contain duplicates, so ascending order here means <=.
	
***
## Brutal Method(先排序，再比较):
<pre><code><em>
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        int[] temp = nums.clone();
        Arrays.sort(temp);     //将数组排序存在temp中
        int start = 0, end = nums.length - 1;
        
        //比较temp
        while (start < nums.length && temp[start] == nums[start]) {  //start小于数组的长度
            start++;
        }
        
        while (end > start && temp[end] == nums[end]) {  //注意这里end要大于start
            end--;
        }
        
        return end -start + 1;
    }
}
</em></code></pre>

* 解题思路：先将数组排序存入temp数组，再比较temp数组和nums。找到不一样的数位。
* 注意：从前往后开始比较不一样的开始位，从后往前比较不一样的结束位<strong>（在这里要注意end不能小于start）。</strong>
* 算法复杂度比较高：排序有O(nlogn)吗，比较有O(n)。空间复杂度为O（n）。

***
## 优化算法（O(n) time O(1) space）：
<pre><code>
<em>
class Solution {
public int findUnsortedSubarray(int[] nums) {
    int n = nums.length;
    int beg = -1;     //存储未排序子数组的开始元素
    int end = -2;     //存储未排序子数组的结束元素
    int min = nums[n-1];   //正序时表示的最大值
    int max = nums[0];     //逆序时表示的最小值
   
    for (int i=1; i<n; i++) {
    	max = Math.max(max, nums[i]);
     	min = Math.min(min, nums[n-1-i]);
        if (nums[i] < max) {
      		end = i;
        }
        if (nums[n-1-i] > min) {
            beg = n-1-i; 
        }   
    }
    return end - beg + 1;
    }
}
</em>
</code></pre>

* 此解法的思路如果数组是按照顺序排好的话，第i个数应该是前i个数中最大的最大值，若不是，则不满足要求。
* 反之，从后往前看，第n-1-i个数应该是后n-1-i个书中最小的最小值。
* 因此维护beg和end两个变量，将不满足上述条件的元素位置赋值给两个变量。