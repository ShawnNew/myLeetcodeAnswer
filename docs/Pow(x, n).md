## 50. Pow(x, n)

Implement pow(x, n).


**Example 1:**

```
Input: 2.00000, 10
Output: 1024.00000
```
**Example 2:**

```
Input: 2.10000, 3
Output: 9.26100
```

### Code:

```java
class Solution {
    public double myPow(double x, int n) {
        if(n == 0) return 1.;
        double res = myPow(x, n / 2);
        return n % 2 == 0 ? res * res : n < 0 ? res * res * (1 / x) : res * res * x;
    }
}
```

### 解题思路：
* 使用递归的思想，x^n = x^(n/2) * x^(n/2)。
* 分情况讨论：
	* n为偶数，```myPow(x, n/2) * myPow(x, n/2);```
	* n为奇数且小于零，```myPow(x, n/2) * myPow(x, n/2) * 1/x;```
	* n为奇数且大于零，```myPow(x, n/2) * myPow(x, n/2) * x;```