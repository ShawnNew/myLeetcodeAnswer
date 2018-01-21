## 78. Subsets

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### Code:

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        result.add(new ArrayList<Integer>());
        backtrack(result, new ArrayList<Integer>(), nums, 0);
        return result;
    }
    
    public void backtrack(List<List<Integer>> result, List<Integer> current, int[] nums, int start) {
        for (int i = start; i < nums.length; i++) {
            current.add(nums[i]);
            result.add(new ArrayList<Integer>(current));
            backtrack(result, current, nums, i+1);
            current.remove(current.size() - 1);
        }
        return;
    }
}
```

### 解题思路

* 使用递归，在自每一次调用递归之前返回可行解。