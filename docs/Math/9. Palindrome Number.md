## 9. Palindrome Number
Determine whether an integer is a palindrome. Do this without extra space.

### Code:
<pre><code>class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x != 0 && x % 10 == 0)) return false;
        int temp = 0;
        while (x > temp) {
            temp = temp * 10 + x % 10;
            x /= 10;
        }
        return (x == temp || x == temp / 10);
    }
}
</code></pre>

***
### 解题思路
* 将数字分成前后两半部分，前半部分正序，后半部分reverse；
* 比较分割后的两个数。