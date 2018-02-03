## 12. Integer to Roman

Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

### Code:

```java
```java
class Solution {
    public String intToRoman(int num) {
        StringBuilder sb = new StringBuilder();
        int[] base = {1000, 900, 500 ,400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] str = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        
        while (num != 0) {
            for (int i = 0; i < base.length; i++) {
                if (base[i] <= num) {
                    num -= base[i];
                    sb.append(str[i]);
                    break;
                } else continue;
            }
        }
        return sb.toString();
    }
}```
```

### 解题思路

* 罗马数字的基本型为：I=1，V=5，X=10，L=50，C=100，D=500，M=1000；
* 因为相同的罗马数字最多不能超三个，所以对于4只能表示为5-1即IV，左减右加。
* 使用贪心算法，每次尽量匹配最大值得到罗马数字；
* 匹配的字符串表为：```{M=1000, 900=CM, 500=D, 400=CD, 100=C, 90=XC, 50=L, 40=XL, 10=X, 9=IX, 5=V, 4=IV, 1=I}```。
