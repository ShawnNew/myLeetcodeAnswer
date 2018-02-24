## 453. Minimum Moves to Equal Array Elements

Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.

**Example:**
```
Input:
[1,2,3]

Output:
3

Explanation:
Only three moves are needed (remember each move increments two elements):

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

#### Code:
```java
class Solution {
    public int minMoves(int[] nums) {
        int len = nums.length;
        int sum = 0, minNum = Integer.MAX_VALUE;
        for (int i : nums) {
            sum += i;
            minNum = Math.min(minNum, i);
        }
        return sum - len * minNum;
    }
}
```

***
#### 解题思路：
* 本题是一个数学问题：根据变化前后以及move的特点列数组和的方程如下，```sum + move * (n-1) = x * n```其中sum是move前的数组累加和，n是数组的长度，x是move后的数组相同元素的大小；
* 并且有如下辅助方程：```x = minNum + m```minNum是move前的数组中的最小数。此处注意**每次变化最小数都会加一，最后得到的数位minNum+m。**
