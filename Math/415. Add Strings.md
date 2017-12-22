## 415. Add Strings

Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

#### Code:
```java
class Solution {
    public String addStrings(String num1, String num2) {
        StringBuilder sb = new StringBuilder();
        int i = num1.length() - 1, j = num2.length() - 1, carry = 0;
        while (i >= 0 || j >= 0) {
            int tempSum = carry;
            if (i >= 0) tempSum += num1.charAt(i--) - '0';
            if (j >= 0) tempSum += num2.charAt(j--) - '0';
            sb.append(tempSum % 10);
            carry = tempSum / 10;
        }
        if (carry != 0) sb.append(carry);
        return sb.reverse().toString();
    }
}
```

***
#### 解题思路：
* 用carry记录进位情况，对于字符串从后向前按位累加；
* 使用StringBuilder存储两数的和。