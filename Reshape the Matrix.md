## Reshape the Matrix

In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data.

You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.

The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.



<pre><code><em>
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        if (nums.length * nums[0].length != r * c) return nums;
        
        int[][] res = new int[r][c];
        int newRow = 0, newCol = 0;
        for (int row = 0; row < nums.length; row++) {  //遍历行 
            int col = 0;
            while (col < nums[0].length) {
                if (newCol < c) {   //新数组每一行内部
                    res[newRow][newCol++] = nums[row][col++];
                    
                } else if (newCol == c) {   //新数组换行
                    newCol = 0;
                    res[++newRow][newCol] = nums[row][col];
                } 
            }  
        }
        return res;
    }
}
</em></code></pre>

***
* 该题的解法是对原数组的每个元素遍历，依次放入新数组中。
* 在放数的时候判断两种情况：
	1. 当前元素是新数组中每一行中间的元素；
	2. 当前元素是新数组中每一行的第一个元素。
	3. 注意，在新数组的列数达到尾部时，老数组的指针已经指向下一个元素，只用把新数组的列数置零，行数加一，最后将元素加入新数组。