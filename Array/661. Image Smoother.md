## Image Smoother

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.

<strong>Example 1:</strong>
<pre>
<strong>Input:</strong>
[[1,1,1],
 [1,0,1],
 [1,1,1]]
<strong>Output:</strong>
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
<strong>Explanation:</strong>
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0
</pre>

<strong>Note:</strong>

* The value in the given matrix is in the range of [0, 255].
* The length and width of the given matrix are in the range of [1, 150].

### 原始算法：
<pre><code>
class Solution {
    public int[][] imageSmoother(int[][] M) {
        int[][] res = new int[M.length][M[0].length];
        int number, sum;
        for (int i = 0; i < M.length; i++) {
            for (int j = 0; j < M[0].length; j++) {
                sum = M[i][j];  //当前元素
                number = 1;
                if (j - 1 >= 0) {  //左边元素
                    number++;
                    sum += M[i][j - 1];
                    if (i - 1 >= 0) {  //左上元素
                        number++;
                        sum += M[i - 1][j - 1];
                    }
                } 
                if (i - 1 >= 0) {  //下边元素
                    number++;
                    sum += M[i - 1][j];
                    if (j + 1 < M[0].length) {  //右上元素
                        number++;
                        sum += M[i - 1][j + 1];
                    }
                }
                if (j + 1 < M[0].length) {    //右边元素
                    number++;
                    sum += M[i][j + 1];
                    if (i + 1 < M.length) {   //右下元素
                        number++;
                        sum += M[i + 1][j + 1];
                    }
                }
                if(i + 1 < M.length) {   //下方元素
                    number++;
                    sum += M[i + 1][j];
                    if (j - 1 >= 0) {   //左下元素
                        number++;
                        sum += M[i + 1][j - 1];
                    }
                }
                
                res[i][j] = (int) Math.floor(sum / number); 
            }
        }
        return res;
    }
}
</code></pre>  

***
* 解决该题的原始算法比较暴力，就是对于数组遍历时的每一个元素的周围八个元素都检查是否存在，若存在则加入sum，并且number++。
* 注意在检查周围八个元素的时候要按顺序，即按照顺时针或者逆时针的方向检查，可以避免多加或者漏加元素。
* 一定要在新数组中进行赋值，避免改变了原始数组元素后操作错误。