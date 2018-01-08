## 33. Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

### Code:

```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums.length == 0) return -1;
        
        int len = nums.length;
        int indexMax = len - 1;
        int start = 0, end = len - 1;
        
        // find the pivot position
        for (int i = indexMax; i > 0; --i) {
            if (nums[i] < nums[i - 1]) indexMax = i - 1;
        }
        
        // change the start and/or end index if the array has been rotated
        if (indexMax != len - 1) {
            if (target >= nums[0]) end = indexMax;
            else start = indexMax + 1;
        }
        
        // do binary search
        while (start+1 < end) {
            int half = (start + end) >>> 1;
            if (nums[half] == target) return half;
            else if (nums[half] < target) start = half;
            else end = half;
        }
        
        if (nums[end] == target) return end;
        if (nums[start] == target) return start;
        return -1;
    }
}
```

### 解题思路：
* 旋转后的数组在pivot两边分别是排序好的，因此可以考虑找到pivot的位置，并且判断之后选择在左边或者右边进行二分查找；
* 数组是在最大值处旋转，因此如果最大值不在数组的尾部，则改变二分查找的范围；
* 二分循环结束，判断end和start两点是否等于target再输出。