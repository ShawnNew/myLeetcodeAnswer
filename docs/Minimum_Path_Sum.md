## 64. Minimum Path Sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

**Example 1:**

```
[[1,3,1],
 [1,5,1],
 [4,2,1]]
```
Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.

### Code:

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                int top = i-1 < 0 ? Integer.MAX_VALUE : grid[i-1][j];
                int left = j-1 < 0 ? Integer.MAX_VALUE : grid[i][j-1];
                if (top == Integer.MAX_VALUE && left == Integer.MAX_VALUE) continue;
                else grid[i][j] = grid[i][j] + Math.min(top, left);
            }
        }
        return grid[row-1][col-1];
    }
}
```

### 解题思路
* 该题使用动态规划的思想，到达终点的最小路径就是从上方走的路径和从左边走的路径的最小值；
* 遍历矩阵，在每一个点上判断上方路径和左边路径的最小值，然后加到该点上；
* 注意对于边界情况的判断，如果超出边界赋值为最大整数，左上角的情况需要特殊讨论。