## 507. Perfect Number
We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.
**Example:**

```
Input: 28
Output: True
Explanation: 28 = 1 + 2 + 4 + 7 + 14
```
### Code:
```java
class Solution {
    public boolean checkPerfectNumber(int num) {
        if (num == 1) return false;
        int sum = 0;
        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) sum += i + num / i;
        }
        sum++;
        return sum == num;
    }
}
```
***
### 解题思路：
* 一个数的除数在sqrt(n)左右两边应该是对称的，所以只要查找小于sqrt(n)的数并且记录其和，最后比较是否等于该数即可。