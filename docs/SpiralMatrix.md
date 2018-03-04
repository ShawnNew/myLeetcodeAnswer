## 54. Spiral Matrix
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

You should return [1,2,3,6,9,8,7,4,5].

### Code:

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<Integer>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return res;
        
        int colStart = 0;
        int colEnd = matrix[0].length-1;
        int rowStart = 0;
        int rowEnd = matrix.length-1;
        
        while (rowStart <= rowEnd && colStart <= colEnd) {
            for (int i = colStart; i <= colEnd; i++) {
                res.add(matrix[rowStart][i]);
            }
            rowStart++;
            for (int i = rowStart; i <= rowEnd; i++) {
                res.add(matrix[i][colEnd]);
            }
            colEnd--;
            if (rowStart <= rowEnd) {
                for (int i = colEnd; i >= colStart; i--) res.add(matrix[rowEnd][i]);
            }
            rowEnd--;
            
            if (colStart <= colEnd) {
                for (int i = rowEnd; i >= rowStart; i--) res.add(matrix[i][colStart]);
            }
            colStart++;
        }
        return res;
    }
}
```

### 解题思路：
* 按照螺旋的方向遍历二维数组，分别使用rowStart、rowEnd、colStart和colEnd四个变量表示行列遍历时的起止位置；
* 从右往左遍历结束后，rowStart++；
* 再向下遍历，colEnd--；
* 再向左遍历，rowEnd--；
* 最后向上遍历，colStart++；
* 注意在向左和向上遍历的时候，需要保证不重复已经遍历过的行和列。即向左遍历时，不能重复遍历行；
* 向上遍历时，不能重复遍历列。