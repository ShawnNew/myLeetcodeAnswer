## Degree of an Array
Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

<strong>Example 1:</strong>
<pre>
Input: [1, 2, 2, 3, 1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.</pre>

<strong>Example 2:</strong>
<pre>Input: [1,2,2,3,1,4,2]
Output: 6</pre>

####Note:

* nums.length will be between 1 and 50,000.
* nums[i] will be an integer between 0 and 49,999.



<pre><code>
class Solution {
    public int findShortestSubArray(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        Map<Integer, Integer[]> hm = new HashMap<Integer, Integer[]>();
        for (int i = 0; i < nums.length; i++) {
            if (!hm.containsKey(nums[i])) {
                hm.put(nums[i], new Integer[]{1, i, i});   //数组存储分别为：频数，第一次出现索引，最后一次出现索引
                Integer[] temp = hm.get(nums[i]);
                temp[0]++;
                temp[2] = i;
            }
        }
        
        int maxDegree = 0;
        int res = 0;
        for (Integer[] values : hm.values()) {
            if (values[0] > maxDegree) { //当前元素的度大于最大度则更改最大度和更新最小长度
                maxDegree = values[0];
                res = values[2] - values[1] + 1; 
            } else if (values[0] == maxDegree) {  //当前元素的度等于最大度，则比较最小长度并更新
                res = Math.min(values[2] - values[1] + 1, res);
            }
        }
        return res;
    }
}</code></pre>

***
* 该题的思路是使用HashMap存储数组中的元素，并且将其频数以及第一次出现位置的索引和最后一次出现次数的索引。HashMap< Integer, Integer[] >
* 再遍历HashMap，找到最大频数，根据索引值算出长度。