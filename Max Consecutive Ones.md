## Max Consecutive Ones

Given a binary array, find the maximum number of consecutive 1s in this array.

#### Example 1:

<pre><code>
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
</code></pre>

#### Note:

* The input array will only contain 0 and 1.
* The length of input array is a positive integer and will not exceed 10,000

<pre><code>
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int res = 0;
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {          
                res = res > count ? res : count;
                count = 0;
            } else if (nums[i] != 0 && i + 1 == nums.length) {    //注意这里的条件是当前位不为零和当前位为是末位
                count += 1;    //计数器加一操作要先于返回值赋值操作
                res = res > count ? res : count;
            } else {
                count += 1;
            }
        }
        return res;
    }
}
</code></pre>
*** 

* 该题的思路是维护两个变量count和res。res记录的是1连续出现的最大个数，count记录的是数组中每一段连续1的个数。
* 遍历数组，遇到0时将count置零后重新计数。
* 注意数组结束时候的判断条件为，当前元素是否为末尾元素并且当前元素不为零。<em>在当前元素在末尾位置时，一定注意要先对计数器加一再赋值。</em>


