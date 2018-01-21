## 77. Combinations

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

### Code

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        backtrack(result, new ArrayList<Integer>(), n, k, 1); //最后一个参数是为了考虑输出结果顺序的影响，避免[a,b]和[b,a]的情况
        return result;
    }
    
    public void backtrack(List<List<Integer>> result, List<Integer> current, int n, int k, int start) {
        if (current.size() == k) result.add(new ArrayList<Integer>(current));
        for (int i = start; i <= n; i++) {
            current.add(i);
            backtrack(result, current, n, k, i+1);
            current.remove(current.size() - 1);
        }
    }
}
```

### 解题思路
因为题目的意思是找到k维的组合，因此要**忽略元素顺序不同，同时元素不能重复。**

* 递归时传入上一层的位置，为了避免在下一层解空间中出现元素次序上的重复；
* 不用重新使用列表存储每一层解空间的可行解，因为根据题目的意思是取1-n的整数，因此直接循环遍历到n的所有元素即可。 