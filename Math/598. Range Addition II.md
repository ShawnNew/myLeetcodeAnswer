## 598. Range Addition II

Given an m * n matrix M initialized with all 0's and several update operations.

Operations are represented by a 2D array, and each operation is represented by an array with two positive integers a and b, which means M[i][j] should be added by one for all 0 <= i < a and 0 <= j < b.

You need to count and return the number of maximum integers in the matrix after performing all the operations.

**Example 1:**

```
Input: 
m = 3, n = 3
operations = [[2,2],[3,3]]
Output: 4
Explanation: 
Initially, M = 
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]

After performing [2,2], M = 
[[1, 1, 0],
 [1, 1, 0],
 [0, 0, 0]]

After performing [3,3], M = 
[[2, 2, 1],
 [2, 2, 1],
 [1, 1, 1]]

So the maximum integer in M is 2, and there are four of it in M. So return 4.
```

### Code:


```java
class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        if (ops.length == 0) return m * n;
        int[] minArea = {Integer.MAX_VALUE, Integer.MAX_VALUE};
        for (int[] op : ops) {
            if (op[0] < minArea[0] || op[1] < minArea[1]) {
                minArea[0] = Math.min(op[0], minArea[0]);
                minArea[1] = Math.min(op[1], minArea[1]);
            }
        }
        return minArea[0] * minArea[1];
    }
}
```

***
### 解题思路：
* 该题可以转换成求相交面积最小的操作；
* 维护一个数组minArea，遍历操作ops，如果操作中的元素小于minArea，则更新minArea；
* 返回minArea的面积即可。