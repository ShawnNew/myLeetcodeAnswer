## Single Number
Given an array of integers, every element appears twice except for one. Find that single one.

<strong>Note:</strong>
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

### 原始代码（HashMap）
<pre><code>
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> hm = new HashMap<Integer, Integer>();
        int res = 0;
        for (int i : nums) {
            hm.put(i, hm.getOrDefault(i, 0) + 1);
        }
        
        for (Map.Entry<Integer, Integer> entry : hm.entrySet()) {
            if (entry.getValue() == 1) {
                res = entry.getKey();
            }
        }
        return res;
    }
}
</code></pre>

***
* 该题的基本思路是将数组遍历后，把元素和其出现次数存入HashMap中。
* 之后再对HashMap进行遍历，找到出现次数为一的元素并返回。