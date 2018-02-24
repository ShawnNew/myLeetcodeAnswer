## 15. 3Sum

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:** The solution set must not contain duplicate triplets.

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

### 原始解法（超时）

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        for (int i=0; i < nums.length; i++) {
            int[] temp = Arrays.copyOfRange(nums, i+1, nums.length);
            twoSum(result, temp, nums[i], -nums[i]);
        }
        return result;
    }
    
    public void twoSum(List<List<Integer>> result, int[] temp, int current, int target) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < temp.length; i++) {
            if (!map.containsKey(temp[i])) map.put(temp[i], i);
            if (map.containsKey(target-temp[i]) && i != map.get(target-temp[i])) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(current);
                list.add(temp[i]);
                list.add(target - temp[i]);
                if (!result.contains(list)) result.add(list);
            }
        }
    }
}
```

### 双指针解法

```java
   public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i-1] ) continue;
            
            int left = i + 1, right = nums.length - 1;
            int target = -nums[i];
            while (left < right) {
                if (nums[left] + nums[right] == target) {
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left++; right--;
                    while (left < right && nums[left] == nums[left-1]) left++;
                    while (left < right && nums[right] == nums[right+1]) right--;
                } else if (nums[left] + nums[right] > target) right--;
                else left++;
            }
        }
        return res;
    }
}
```

### 解题思路
* 先对数组进行排序，在遍历每个元素时如果发现重复，则跳过；
* 在遍历每个元素时，再使用left和right指针以及目标-nums[i]找满足条件的元素；
* 因为数组是排序过的，所以可以从两头往中间找；
* 相加结果如果大于目标，则移动右边指针；
* 如果小于目标，则移动左边目标；
* 如果等于目标，则将三维数组加入结果列表；
* 找到目标后同时移动两边指针，并且跳过重复元素。