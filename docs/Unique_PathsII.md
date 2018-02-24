## 63. Unique Paths II
Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.

```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```
The total number of unique paths is 2.

**Note:** m and n will be at most 100.

### Code:

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int row = obstacleGrid.length;
        int col = obstacleGrid[0].length;
        obstacleGrid[0][0] = obstacleGrid[0][0] == 1 ? 0 : 1; //左上角元素反转
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (i == 0 && j == 0) continue;     //跳过左上角元素
                if (obstacleGrid[i][j] == 1) obstacleGrid[i][j] = 0;   //如果当前元素初始值为1，则将其值赋0
                else {
                    int top = i-1 < 0 ? 0 : obstacleGrid[i-1][j];
                    int left = j-1 < 0 ? 0 : obstacleGrid[i][j-1];
                    obstacleGrid[i][j] = top + left;
                }
            }
        }
        return obstacleGrid[row-1][col-1];
    }
}
```

### 解题思路
* 遍历矩阵，每个元素的值为上方值加左边的值，如果上方或者左边超出边界，则加0；
* 初始情况对左上角元素反转，在遍历的过程中跳过左上角元素。