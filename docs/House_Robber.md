## 198. House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### Code

```java
class Solution {
    public int rob(int[] nums) {
        int prevNo = 0, prevYes = 0;
        for (int num : nums) {
            int temp = prevNo;
            prevNo = Math.max(prevNo, prevYes);
            prevYes = temp + num;
        }
        
        return Math.max(prevNo, prevYes);
    }
}
```

### 解题思路
* 维护两个变量，prevNo和prevYes，分别表示没有rob上一家的最大值和rob了上一家的最大值；
* 在遍历的当前家，更新prevNo为prevNo和prevYes的最大值，因为prevNo和prevYes都没有包含当前住户；
* prevYes更新为prevNo+nums[i]，因为要保证没有警报，必须有上一家没有被rob；
* 考虑到更新prevNo时改变了值但是之后要使用其值，所以在更改变量之前先保存其值为temp。