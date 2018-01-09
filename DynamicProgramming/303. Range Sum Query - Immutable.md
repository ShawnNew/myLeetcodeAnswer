## 303. Range Sum Query - Immutable

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

**Example:**

```
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

### Code

```java
class NumArray {
    int cumArray[];
    public NumArray(int[] nums) {
        for (int i = 1; i < nums.length; i++) {
            nums[i] += nums[i-1];
        }
        this.cumArray = nums;
    }
    
    public int sumRange(int i, int j) {
        if (i == 0) return cumArray[j];
        return cumArray[j] - cumArray[i - 1];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```

### 解题思路：
* 在类中定义一个成员变量cumArray，用来记录每一位的累加值；
* sumRange就是```cumArray[j] - cumArray[i - 1];```