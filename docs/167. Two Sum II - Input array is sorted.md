## Two Sum II - Input array is sorted

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

<pre><code>
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] result = new int[2];
        if (numbers == null || numbers.length < 2) {  //特殊情况
            return result;
        }        
        
        int indFirst = 0;                 //定义左右指针
        int indSecond = numbers.length - 1;
        
        while (indSecond > indFirst) {
            int sum = numbers[indSecond] + numbers[indFirst];
            if (sum == target) {
                result[0] = indFirst + 1;
                result[1] = indSecond + 1;
                break;                 //跳出循环
            } else if (sum > target) {
                indSecond--;
            } else {
                indFirst++;
            }
        }
        
        return result;
    }
}
</code></pre>

* 给定已排序数组的问题，往往解题方向是从两边开始往中间解决问题。
* 维护头尾两个指针，头尾指针所对应的数组元素之和和target进行比较，如果满足条件直接输出头尾指针，如果不满足，则移动头尾指针。
* 元素之和大于target，则移动尾指针；元素之和小于target，则移动头指针。