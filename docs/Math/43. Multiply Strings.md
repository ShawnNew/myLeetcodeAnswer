## 43. Multiply Strings

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.

**Note:**

1. The length of both num1 and num2 is < 110.
2. Both num1 and num2 contains only digits 0-9.
3. Both num1 and num2 does not contain any leading zero.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

### Code

```java
class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length(), len2 = num2.length();
        int[] mul = new int[len1+len2];
        for (int i = len1-1; i >= 0; i--) {
            for (int j = len2-1; j >= 0; j--) {
                int p1 = i + j;    //高位数字
                int p2 = i + j + 1; //低位数字
                int temp = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                int num = temp + mul[p2];
                mul[p1] += num / 10;  
                mul[p2] = num % 10;
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (int i : mul) {
            if (!(i == 0 && sb.length() == 0)) sb.append(i);
        }
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```

### 解题思路

* 按照正常的乘法逻辑，从右往做遍历每位数，i+j+1是低位，i+j是高位；
* 在遍历时，两个数的对应位的数相乘；
* 所得和的十位存入高位，个位存入低位。