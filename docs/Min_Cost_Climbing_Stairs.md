## 746. Min Cost Climbing Stairs

On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

**Example 1:**

```
Input: cost = [10, 15, 20]
Output: 15
Explanation: Cheapest is start on cost[1], pay that cost and go to the top.
```
**Example 2:**

```
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].
```
**Note:**

* cost will have a length in the range [2, 1000].
* Every cost[i] will be an integer in the range [0, 999].

### Code:

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int prevOne = 0, prevTwo = 0;
        for (int cst : cost) {
            int temp = prevOne;
            prevOne = Math.min(prevOne + cst, prevTwo + cst);
            prevTwo = temp;
        }
        return Math.min(prevOne, prevTwo);
    }
}
```

### 解题思路
* 该题使用动态规划，考虑维护两个前一状态变量prevOne和prevTwo;
* prevOne指前一个元素的cost，prevTwo指前两个元素的cost；
* prevOne更新为```Math.min(prevOne+cost, prevTwo+cost);```
* prevTwo更新为前一状态的prevOne。
