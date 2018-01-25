## 16. 3Sum Closest

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
### Code

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int len = nums.length;
        int min = nums[0] + nums[1] + nums[len-1];
        Arrays.sort(nums);
        for (int i = 0; i < len-2; i++) {
            int left = i + 1;
            int right = len - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum>target) right--;
                else left++;
                if (Math.abs(sum - target) < Math.abs(min - target))
                    min = sum;
            }
        }
        return min;
    }
}
```

### 解题思路
* 使用双指针的方法，先对数组进行排序；
* 在遍历数组的时候，从下一元素到结尾的子数组中找两个与target相差最小的元素；
* 然后移动外层遍历元素。