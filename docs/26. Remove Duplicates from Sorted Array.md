### Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.
Do not allocate extra space for another array, you must do this in place with constant memory.

For example,

Given input array nums = [1, 1, 2],
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.
<pre><code>
public class Solution {
    public int removeDuplicates(int[] nums) {
        int newPoint = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != nums[newPoint]) {
                newPoint++;
                nums[newPoint] = nums[i];
            }
        }
        return newPoint + 1;
    }
}
</code></pre>

* 双指针法：定义两个快慢指针，快指针遍历数组，慢指针存储新的元素。
