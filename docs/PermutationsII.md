## 47. Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
[1,1,2] have the following unique permutations:

```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

### Code:

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> numsList = new ArrayList<Integer>();
        for (int i = 0; i < nums.length; i++) numsList.add(nums[i]);
        trackback(result, new ArrayList<Integer>(), numsList);
        return result;
    }
    
    public void trackback(List<List<Integer>> result, List<Integer> current, List<Integer> nums) {
        if (nums.size() == 0) result.add(new ArrayList<Integer>(current));
        
        if (nums.size() > 0) {
            for (int i = 0; i < nums.size(); i ++) {
                List<Integer> space = new ArrayList<Integer>(nums);
                if (nums.subList(0, i).contains(nums.get(i))) {  // 如果该元素在之前的数组中出现过，则跳过
                    continue;
                } else {
                    current.add(nums.get(i));
                    space.remove(i);
                    trackback(result, current, space);
                    current.remove(current.size()-1);
                }
            }
        }
    }
}
```

### 解题思路
思路同[LeetCode 46（Permutations）](https://github.com/ShawnNew/myLeetcodeAnswer/blob/master/BackTracking/46.%20Permutations.md) :clap: :clap:

* 在每一层的解空间，如果遍历元素在该元素之前的subList中出现过，则跳过当前遍历元素。 