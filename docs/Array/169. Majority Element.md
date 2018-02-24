## Majority Element
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

<pre><code>
class Solution {
    public int majorityElement(int[] nums) {
        int elem = 0;        //记录元素
        int counter = 0;     //元素计数，如果相同则加一，不同则减一
        
        for (int i = 0; i < nums.length; i++) {
            if (counter == 0) {
                elem = nums[i];
                counter = 1;
            } else {
                if (elem == nums[i]) {
                    counter++;
                } else {
                    counter--;
                }
            }
        }
        return elem;
    }
}
</code></pre>

* majority element的总数减去其他元素的总和大于等于1。
* 定义一个计数器，用来对相同元素计数。相同元素计数器加一，不同元素计数器减一。更新元素。
* 遍历数组，majority element的计数总是大于等于1，返回该元素。