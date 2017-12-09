## 594. Longest Harmonious Subsequence
We define a harmonious array is an array where the difference between its maximum value and its minimum value is exactly 1.

Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.
<strong>Example:</strong>
<pre>Input: [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].</pre>

### Code:
<pre><code>class Solution {
    public int findLHS(int[] nums) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        int res = 0;
        for (int i : nums) map.put(i, map.getOrDefault(i, 0) + 1);
        for (Integer key : map.keySet()) {
            if (map.containsKey(key + 1)) res = Math.max(res, map.get(key) + map.get(key + 1)); 
        }
        return res;
    }
}</code></pre>

***
* 解题思路是使用HashMap记录不同元素以及每种元素出现的个数；
* 遍历HashMap，对每一种元素找到差为一的元素，并计算subsequence的个数并且更新返回值。
