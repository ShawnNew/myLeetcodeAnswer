## 168. Excel Sheet Column Title

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

<pre> 
1 -> A
2 -> B
3 -> C
...
26 -> Z
27 -> AA
28 -> AB </pre>

#### Code:
<pre><code>class Solution {
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n != 0) {
            n--;
            sb.append((char) ('A' + n % 26));
            n /= 26;
        }
        return sb.reverse().toString();
    }
}
</code></pre>

***
####解题思路：
* 思路同数与数之间的进制转化，将n转化为26进制数，每一位1-26分别对应A-Z；
* 注意将n-1后取余，这样可以直接得到0-25对应A-Z。