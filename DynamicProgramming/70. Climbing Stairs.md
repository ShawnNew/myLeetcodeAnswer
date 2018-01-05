## 70. Climbing Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.


**Example 1:**

```
Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps
```
**Example 2:**

```
Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

### Code:

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) return 1;
        int prev1 = 1, prev2 = 1, result = 0;
        if (n > 1) {
            for (int i = 2; i <= n; i++) {
                result = prev1 + prev2;
                prev1 = prev2;
                prev2 = result;
            }
        }
        return result;
    }
}
```

### 解题思路
* 使用prev1和prev2两个变量分别记录前两层的情况；
* n=0或者n=1时结果是1；
* 循环2到n，结果为前两层的情况相加，并且更新prev1和prev2的值。