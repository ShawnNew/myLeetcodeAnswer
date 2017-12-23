## 441. Arranging Coins

You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

**Example 1:**

```
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
```
**Example 2:**
```
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```

#### Code:
```java
class Solution {
    public int arrangeCoins(int n) {
        return (int) ((Math.sqrt(1 + 8.0 * n) - 1) / 2);
    }
}
```

***
#### 解题思路
* 该题可以使用二分法求解，同时也可以使用数学方法。
* 数学方法是求解不等方程：(1+x) * x / 2 <= n中x的解；
* 即x = (sqrt(1 + 8*n)-1) / 2;
* 注意8*n如果在n很大的情况下会造成overflow，所以使用double类型可以防止溢出。