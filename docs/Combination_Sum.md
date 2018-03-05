## 39. Combination Sum


Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

**Note:**

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.
For example, given candidate set [2, 3, 6, 7] and target 7, 
A solution set is: 

```
[
  [7],
  [2, 2, 3]
]
```

### Code:

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        backtrack(result, new ArrayList<Integer>(), candidates, target, 0);
        return result;
    }
    
    public void backtrack(List<List<Integer>> result, List<Integer> current, int[] candidates, int target, int start) {
        if (target == 0) result.add(new ArrayList<Integer>(current));
        if (target > 0) {
            for (int i = start; i < candidates.length; i++) {
                current.add(candidates[i]);
                backtrack(result, current, candidates, target-candidates[i], i);
                current.remove(current.size() - 1);
            }
        }
    }
    
}
```

### 解题思路
* 递归得使用回溯法；
* 每次添加一个数进入列表，则target减去所添加的数，因此递归的终止条件，是target等于零时；
* 为了避免重复，每一层的调用起始点从上一层的索引位置开始，这样在遍历新层的时候就避免了因为顺序不同而带来的重复。
