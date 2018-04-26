## 41. First Missing Positive

Given an unsorted integer array, find the smallest missing positive integer.

**Example 1:**

```
Input: [1,2,0]
Output: 3
```

**Example 2:**

```
Input: [3,4,-1,1]
Output: 2
```

**Example 3:**

``
Input: [7,8,9,11,12]
Output: 1
```

**Note:**

Your algorithm should run in O(n) time and uses constant extra space.

### Code

```java
class Solution {
    /*
    将符合条件的整数重新排列在数组nums中（前len(nums)个，正的）。
    然后再遍历nums数组，找到其中元素不等于其索引值的位置返回。
    */
    public int firstMissingPositive(int[] nums) {
        int i = 0;  // Index of the element
        while (i < nums.length) {
            if (nums[i] == i+1 || nums[i] <= 0 || nums[i] > nums.length) i++;
            else if (nums[i] != nums[nums[i]-1]) swap(nums, i, nums[i]-1);
            else i++;
        }
        
        i = 0;
        while (i < nums.length && nums[i] == i+1) i++;
        return i+1;
    }
    
    public static void swap(int[] nums, int i, int j) {
        //Swap two elements indexed by i and j in an array.
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

### 解题思路
* 分析这道题目，可以看出最小的正整数一定在数组长度的范围内（nums.length）；
* 因此，将正整数挪动到其对应的索引位：3-->nums[2]；
* 对于负数，或者值大于数组长度的数可以忽略；
* 从数组的头开始，找到不满足`i+1 == nums[i]`的位置，`i+1`即是缺少的最小整数。