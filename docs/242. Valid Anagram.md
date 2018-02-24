## Valid Anagram
Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

<strong>Note:</strong></br>
You may assume the string contains only lowercase alphabets.

<strong>Follow up:</strong></br>
What if the inputs contain unicode characters? How would you adapt your solution to such case?

<pre><code>
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        int[] m1 = new int[128];
        int[] m2 = new int[128];
        
        for (int i = 0; i < s.length(); i++) {
            m1[s.charAt(i)] += 1;
            m2[t.charAt(i)] += 1;
        }
        
        for (int i = 0; i < m1.length; i++) {
            if (m1[i] != m2[i]) return false;
        }
        return true;
    }
}
</code></pre>

***
* 定义128位数组，分别对应每个字符；
* 对两个字符串每位字符出现次数计数；
* 比较每种字符的计数是否相等，如果不相等则返回false。