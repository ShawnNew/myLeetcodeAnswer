## 263. Ugly Number
Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.

#### Code:
<pre><code>class Solution {
    public boolean isUgly(int num) {
        for (int i = 2; i < 6 && num > 0; i++) {
            while (num % i == 0)
                num /= i;
        }
        return num == 1;
    }
}
</code></pre>

***
#### 解题思路：
* 循环查看数字是否能被2、3、4和5整除，如果整除就将数赋值为商；
* 检查循环结束，数是否等于1.