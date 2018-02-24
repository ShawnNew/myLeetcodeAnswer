## Word Pattern
Given a pattern and a string str, find if str follows the same pattern.

Here <strong>follow</strong> means a full match, such that there is a bijection between a letter in pattern and a <strong>non-empty</strong> word in str.

<strong>Examples:</strong>
 
 1. pattern = "abba", str = "dog cat cat dog" should return true.
 2. pattern = "abba", str = "dog cat cat fish" should return false.
 3. pattern = "aaaa", str = "dog cat cat dog" should return false.
 4. pattern = "abba", str = "dog dog dog dog" should return false.

<strong>Notes:</strong></br>
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

### Code:
<pre><code>
class Solution {
    public boolean wordPattern(String pattern, String str) {
        Map hm = new HashMap();  //定义HashMap，存入pattern类型
        String[] strSplit = str.split(" ");   //分割字符串
        
        if (strSplit.length != pattern.length()) return false;  //pattern和单词组不等长，返回false
        
        for (Integer i = 0; i < strSplit.length; ++i) {  //遍历pattern
            if (hm.putIfAbsent(pattern.charAt(i), i) != hm.putIfAbsent(strSplit[i], i)) return false;    
        }
        return true;
    }
}
</code></pre>

***
* 该题考虑使用HashMap，但是注意pattern和word的一一对应（不能只考虑单方面对应）。
* 可以将pattern和word都存入HashMap中，用索引值作为其value值，比较索引值如果不同则返回false。
* 此处使用了HashMap的内建函数hm.putIfAbsent(key, value)，如果不存在则存入，存在则返回value值。