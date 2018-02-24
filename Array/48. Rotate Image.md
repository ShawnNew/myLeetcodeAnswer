## 48. Rotate Image

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Note:**
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

**Example 1:**

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**Example 2:**

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

### Code：

```java
class Solution {
    public void rotate(int[][] matrix) {
        int len = matrix.length;
        
        // reverse the matrix vertically
        for (int i = 0; i < len/2; i++) {  // i loop to len/2
            for (int j = 0; j < len; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[len-i-1][j];
                matrix[len-i-1][j] = temp;
            }
        }
        
        // rotate symmetrically
        for (int i = 0; i < len; i++) {
            for (int j = i; j < len; j++) {   // j loop from i
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        
    }
}
```

### 解题思路
* 将矩阵的旋转问题拆分成行交换问题和一个转置问题。
* 首先将矩阵的行进行一次逆变换，再对矩阵进行转置。