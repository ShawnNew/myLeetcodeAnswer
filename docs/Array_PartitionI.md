## Array Partition I

Given an array of 2n integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

#### Example 1 :
<pre><code>
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).
</code></pre>

#### Note :
	1.n is a positive integer, which is in the range of [1, 10000].
	2. All the integers in the array will be in the range of [-10000, 10000].


##<em>解法</em>
<pre><code><em>
class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int pos = 0;
        int res = 0;
        while (pos < nums.length) {
            res += nums[pos];
            pos += 2;
        }
        return res;
    }
}
</em></code></pre>

***
* 理解题干意思，求使数对最小值的累加和最大的数对组合。可以分析该题的解为将数组中两个数值差别最小的两个元素组合为数对，可以满足条件。
* 因此先对数组进行排序。
* 对排序好的数组进行遍历，隔一个数累加一次，最后求得和。