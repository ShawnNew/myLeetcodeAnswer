## 40. Combination Sum II

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

**Note:**

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.
For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, 
A solution set is: 

```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```


### Code:

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        Arrays.sort(candidates);
        backtrack(result, new ArrayList<Integer>(), candidates, target, 0);  //backtrack
        return result;
    }
    public void backtrack(List<List<Integer>> result, List<Integer> current, int[] candidates, int target, int start) {
        if (target == 0) result.add(new ArrayList<Integer>(current));  //if find the optimal solution, add to result
        if (target > 0) {
            int prev = 0;
            for (int i = start; i < candidates.length; i++) {
                if (candidates[i] == prev) {  //skip duplicated number in the same level of sorted candidates array
                    continue;
                } else {
                    current.add(candidates[i]);  //loop each feasible solution of every level
                    backtrack(result, current, candidates, target-candidates[i], i+1);
                    current.remove(current.size()-1);
                    prev = candidates[i];    //record the previous number
                }
                
            }
        }
    }
}
```

### 解题思路：
* 思路同[Leetcode 39 (combination sum)](https://github.com/ShawnNew/myLeetcodeAnswer/blob/master/BackTracking/39.%20Combination%20Sum.md)
* 为了保证同一数字不被重复使用，需在backtrack递归的时候将起始位置加一；
* 并且如果candidates数组中出现相同数字的时候，会造成结果重复，所以需要先对数组进行排序，在遍历每层元素的时候跳过相同元素。