## Isomorphic Strings
Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

<strong>For example,</strong></br>
<em>Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.</em>

### Code:
<pre><code>
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character, Character> hm_s2t = new HashMap<Character, Character>();
        Map<Character, Character> hm_t2s = new HashMap<Character, Character>();
        boolean res = true;
        
        for (int i = 0; i < s.length(); i++) {
            char c_s = s.charAt(i), c_t = t.charAt(i);
            if (!hm_s2t.containsKey(c_s)) {
                hm_s2t.put(c_s, c_t);
            }
            if (!hm_t2s.containsKey(c_t)) {
                hm_t2s.put(c_t, c_s);
            }
            if (hm_s2t.containsKey(c_s) && hm_s2t.get(c_s) != c_t) res = false;
            if (hm_t2s.containsKey(c_t) && hm_t2s.get(c_t) != c_s) res = false;
        }
        return res;
    }
}
</code></pre>

***
* 该题的解题思路是将<code>s->t</code>以及<code>t->s</code>的对应字符存入HashMap；
* 对于两个字符串遍历，若某元素不存在于HashMap，则加入<code>< s.charAt(i), t.charAt(i) ></code>;
* 若某元素存在于HashMap中，找到对应替换元素，若不等于另一个字符串中的字符，则令返回值为false；
* <strong>注意：要分别判断<code>s->t</code>以及<code>t->s</code>两种情况。</strong>

###改进代码：
<pre><code>
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int[] m1 = new int[256]; int[] m2 = new int[256]; int len = s.length();
        for (int i = 0; i < len; i++) {
            if (m1[s.charAt(i)] != m2[t.charAt(i)]) return false;
            m1[s.charAt(i)] = i + 1;
            m2[t.charAt(i)] = i + 1;
        }
        return true;
    }
}
</code></pre>

***
* 用256位数组表示ASCII码表
