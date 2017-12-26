## Find All Numbers Disappeared in an Array

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

<pre><code>
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        int len = nums.length;
        List<Integer> resultList = new ArrayList<Integer>();
        
        if (nums == null || nums.length == 0) {
            return resultList;
        }
        
        //将对应位标负，不影响其值大小
        for (int i = 0; i < nums.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            if (nums[index] > 0) {
                nums[index] = -nums[index];
            }
        }
        
        //二次循环，输出值为正的位对应的值
        for (int i = 0; i < len; i++) {
            if(nums[i] > 0) {
                resultList.add(i + 1);
            }
        }
        
        return resultList;
    }
}
</code></pre>

* 解该题的思路，应该考虑每一位元素值的大小和其在数组总的索引值存在关系：nums[i] = i + 1。但是给定的数组却是乱序存在的。
* 使用标负法，可以将元素对应位的数变为负数却不影响元素绝对值大小，剩下数组中值为正的位即为数组缺少的元素。
* 根据索引与值的关系即可输出缺少元素。