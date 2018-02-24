## 55. Jump Game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:

A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

### Code:

```java
class Solution {
    public boolean canJump(int[] nums) {
        int max = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (max < i) return false;
            max = Math.max(nums[i]+i, max);
        }
        return true;
    }
}
```

### 解题思路
* 在遍历每一位元素时贪心得找到能到达的最远距离；
* 若某一元素的位置索引大于最远距离，则说明当前位置不可达，返回false；
* 递归结束返回true。