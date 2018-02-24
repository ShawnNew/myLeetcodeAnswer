## 645. Set Mismatch
The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.
</br><strong>Example:</strong>
<pre>Input: nums = [1,2,2,4]
Output: [2,3]
</pre>

### Code:
<pre><code>class Solution {
    public int[] findErrorNums(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        int sum = 0;
        int duplicate = 0;
        int[] res = new int[2];
        for (int i : nums) {
            if (!set.add(i)) duplicate = i;
            sum += i;
        }
        res[1] = ((1 + nums.length) * nums.length / 2) - sum + duplicate;
        res[0] = duplicate;
        return res;
    }
}
</code></pre>

***
* 用HashSet存储不重复的元素，如果重复，则记录duplicate，并且在遍历的过程中记录累加和。
* 返回duplicate和duplicate+(1+n)*n/2-sum.