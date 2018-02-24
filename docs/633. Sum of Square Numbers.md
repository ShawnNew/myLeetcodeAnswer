## 633. Sum of Square Numbers

Given a non-negative integer c, your task is to decide whether there're two integers a and b such that a2 + b2 = c.

**Example 1:**

```
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```
**Example 2:**

```
Input: 3
Output: False
```

### Code:

```java
class Solution {
    public boolean judgeSquareSum(int c) {
        for (int i = 0; i <= Math.sqrt(c); i++) {
            int b = (int) Math.sqrt(c - i * i);
            if (b * b == c - i * i) return true;
        }
        return false;
    }
}
```

***
### 解题思路：
* 遍历0到sqrt(n)范围内的整数，满足a^2 + b^2 = c，则返回true，否则返回false；
* 需注意遍历时可以取到i=sqrt(n)。