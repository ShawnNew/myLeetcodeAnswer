## 18. 4Sum

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.


**Note**  The solution set must not contain duplicate quadruplets.


```
For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

###  Code:

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        return kSum(nums, target, 4, 0);
    }
    
    public List<List<Integer>> kSum(int[] nums, int target, int k, int index) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (k == 2) { //2sum
            int start = index, end = nums.length-1;
            while (start < end) {
                if (nums[start] + nums[end] == target) {
                    List<Integer> temp = new ArrayList<Integer>();
                    temp.add(nums[start]);
                    temp.add(nums[end]);
                    res.add(temp);
                    while (start < end && nums[start] == nums[start+1]) start++;  // skip the duplicates
                    while (start < end && nums[end] == nums[end-1]) end--;
                    start++; end--;
                } else if (nums[start] + nums[end] > target) {
                    end--;
                } else start++;
            }
        } else {  // k-1sum
            for (int i = index; i < nums.length-1; i++) {
                List<List<Integer>> temp = kSum(nums, target-nums[i], k-1, i+1);  // recursively get k-1 sum
                if (temp != null) {
                    for (List t : temp) {
                        t.add(0, nums[i]);  // add the current number to the head of the list
                    }
                    res.addAll(temp);
                }
                while (i < nums.length - 1 && nums[i] == nums[i+1]) i++; // skip the duplicates
            }
        }
        return res;   
    }
}

```

### 解题思路
* 使用递归，将kSum转换成k-1Sum，base case是2Sum；
* 对数组进行排序，然后再递归解决；
* 在2Sum和k-1Sum的情况去除重复，如果```nums[i] == nums[i+1];```则```i++;```，需要注意判断条件```i<nums.length-1```；
* 递归式为(k-1)Sum+i,其中i为当前kSum当前遍历元素。
