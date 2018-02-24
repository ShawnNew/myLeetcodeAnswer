## 62. Unique Paths
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![](tupian/uniquePaths.png)

### Code

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] path = new int[m][n];
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 || j == 0) path[i][j] = 1;
                else path[i][j] = path[i-1][j] + path[i][j-1];
            }
        }
        return path[m-1][n-1];
    }
}
```

### 解题思路
* 记录路径矩阵，如上图所示，矩阵的最上边一行和最左边一行都为1；
* 其他部分的元素为上方元素与左边元素相加的和；
* 遍历m*n的所有元素，得到路径矩阵，返回右下角元素。