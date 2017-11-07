## Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

<pre><code>
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> hm = new HashMap<Integer, Integer>();   //定义hashMap用于存放数组中元素
        int[] result = new int[2];                                        //定义result返回值
        for (int i = 0; i < nums.length; i++) {
            int pos = 0;                                                  //pos是满足条件的对应元素的位置
            
            //若hashmap中没有当前元素，则将元素加入hashmap中
            if (!hm.containsKey(nums[i])) {
                hm.put(nums[i], i);
            }
            
            //若hashmap中找到了当前元素，则找出对应满足条件的元素
            if (hm.containsKey(target - nums[i]) && i != hm.get(target - nums[i])) {
                pos = hm.get(target - nums[i]);
                if (i < pos) {
                    result[0] = i;
                    result[1] = pos;
                } else {
                    result[0] = pos;
                    result[1] = i;
                }         
            }      
        }
        return result;
    }
}
</code></pre>

* 使用HashMap可以缩短查找元素的时间，每次查找时间为O(1)。
* 检查HashMap是否有当前遍历元素，不存在则加入HashMap。