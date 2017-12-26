## Move Zeroes

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

<pre><code>
class Solution {
    public void moveZeroes(int[] nums) {
        
        int counter = 0; //计数器记录出现零的个数
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                counter++;  //元素为零，计数器加一
            } else {
                nums[i - counter] = nums[i];  //把当前元素向前移动计数器大小位
            }
        }
        for (int i = 0; i < counter; i++) {
        //在数组后面补上零
            nums[nums.length - counter + i] = 0;
        }
    }
}
</code></pre>

* 维护一个counter，用来记录在数组中出现零的个数。
* 在遍历数组的过程中，将非零元素向前移动计数器大小位。
* 最后在数组后面补上相应的零。