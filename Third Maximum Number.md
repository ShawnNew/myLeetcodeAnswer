## Third Maximum Number

Given a non-empty array of integers, return the third maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).

<pre><code>
class Solution {
    public int thirdMax(int[] nums) {
        int res = 0;
        
        long fmax = Long.MIN_VALUE, smax = Long.MIN_VALUE, tmax = Long.MIN_VALUE;   //初始化的时候注意初始化为long类型的最小值
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > fmax && nums[i] > smax && nums[i] > tmax) {
                tmax = smax;
                smax = fmax;
                fmax = nums[i];
            } else if (nums[i] < fmax && nums[i] > smax && nums[i] > tmax) { 
                tmax = smax;
                smax = nums[i];
            } else if (nums[i] < fmax && nums[i] < smax && nums[i] > tmax) {
                tmax = nums[i];
            }
        }
        
        if (tmax != Long.MIN_VALUE && tmax != smax) {
            res = (int)tmax;   //强制转换
        } else {
            res = (int)fmax;
        }
        return res;
    }
}
</code></pre>

* 该题思路是维护三个变量，分别为前三大的数字，遍历数组改变变量值。
* 注意初始化变量时将其赋值为long类型的最小值--Long.MIN_VALUE。
* 返回结果时使用强制转换将前三大变量输出。