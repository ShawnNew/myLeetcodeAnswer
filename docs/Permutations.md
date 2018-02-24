## 46. Permutations

Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:

```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### Code:

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> numsList = new ArrayList<Integer>();
        for (int i=0; i<nums.length; i++) numsList.add(nums[i]);
        backtrack(result, new ArrayList<Integer>(), numsList);
        return result;
    }
    
    public void backtrack(List<List<Integer>> result, List<Integer> current, List<Integer> nums) {
        if (nums.size() == 0) result.add(new ArrayList<Integer>(current));
        if (nums.size() != 0) {
            for (int i = 0; i < nums.size(); i++) {
                List<Integer> temp = new ArrayList<Integer>(nums);
                current.add(nums.get(i));
                temp.remove(i);
                backtrack(result, current, temp);
                current.remove(current.size() - 1); 
            } 
        }
    }
}
```

### 解题思路
这个题做的很艰辛啊 :see_no_evil: :see_no_evil:

* 使用回溯的方法，每一层解空间为去除当前元素的数组；
* 因此在进入每一层时，为了不影响当前层的解空间的元素，需使用temp列表用来表示传入下一层的解空间；
* 此题的递归终止条件是解空间的维度降为零时，添加一个可行解。