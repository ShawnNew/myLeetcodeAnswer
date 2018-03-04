## 59. Spiral Matrix II

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

### Code

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        
        int rowStart = 0;
        int rowEnd = n-1;
        int colStart = 0;
        int colEnd = n-1;
        
        int num = 1;
        while (rowStart <= rowEnd && colStart <= colEnd) {
            for (int i = colStart ; i <= colEnd; i++) res[rowStart][i] = num++;
            rowStart++;
            
            for (int i = rowStart; i <= rowEnd; i++) res[i][colEnd] = num++;
            colEnd--;
            
            if (rowStart <= rowEnd) {
                for (int i = colEnd; i >= colStart; i--) res[rowEnd][i] = num++;
            }
            rowEnd--;
            
            if (colStart <= colEnd) {
                for (int i = rowEnd; i>= rowStart; i--) res[i][colStart] = num++;
            }
            colStart++;
        }
        
        return res;
    }
}
```

### 解题思路
* 思路同[54. Spiral Matrix](SpiralMatrix.md)
* 按照右下左上的顺序分别遍历数组中的元素，然后存入一个递增的数；
* 使用rowStart、rowEnd、colStart和colEnd分别记录行和列的起止位置。