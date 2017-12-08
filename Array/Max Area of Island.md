## Max Area of Island
Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

<strong>Example 1:</strong>
<pre>[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]] </pre>
 Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.
 
 <strong>Example 2:</strong>
<pre>[[0,0,0,0,0,0,0,0]]</pre>
Given the above grid, return 0.

<strong>Note:</strong> The length of each dimension in the given grid does not exceed 50.

## Code:

<pre><code>
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int maxArea = 0;
        int row = grid.length, col = grid[0].length;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (grid[i][j] == 1) {
                    maxArea = Math.max(maxArea, areaOfIsland(grid, i, j));
                }
            }
        }
        return maxArea;
    }
    
    public int areaOfIsland(int[][] grid, int row, int col) {  //使用递归，检查当前遍历元素是否的最大岛深度
        if (row >= 0 && row < grid.length && col >= 0 && col < grid[0].length && grid[row][col] == 1) {
            grid[row][col] = 0;
            return areaOfIsland(grid,row-1,col)+areaOfIsland(grid,row+1,col)+areaOfIsland(grid,row,col-1)+areaOfIsland(grid,row,col+1)+1;
        }
        return 0;
    }
}
</code></pre>

***
* 该题的解题思路是使用递归进行深度优先遍历（dfs）。
* 在遍历数组的过程中每遇到一个值为一的元素，则对元素的上下左右进行深度优先查找，得到包含该元素的最大岛面积。若大于maxArea则更新。
* 递归函数的返回值为整型的从当前元素出发的最大岛面积。递归的<strong><em><font color=crimson>Base Case</font>是：检查到一个元素为0,则返回0</em></strong>；<strong><em><font color=crimson>递归式为：</font>areaOfIsland(左边元素)+areaOfIsland(右边元素)+areaOfIsland(上边元素)+areaOfIsland(下边元素)+1。</em></strong>
