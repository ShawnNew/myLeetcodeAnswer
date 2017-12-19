## 258. Add Digits
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

<pre><code>class Solution {
    public int addDigits(int num) {
        return 1 + (num - 1) % 9;
    }
}
</code></pre>

***
#### 解题思路：
* Input:0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,...
* Output:0,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,...