## 720. Longest Word in Dictionary
Given a list of strings words representing an English Dictionary, find the longest word in words that can be built one character at a time by other words in words. If there is more than one possible answer, return the longest word with the smallest lexicographical order.

If there is no answer, return the empty string.

<strong>Example 1:</strong>
<pre>Input: 
words = ["w","wo","wor","worl", "world"]
Output: "world"
Explanation: 
The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
</pre>

<strong>Example 2:</strong>
<pre>Input: 
words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]
Output: "apple"
Explanation: 
Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".</pre>

### Code:
<pre><code>class Solution {
    public String longestWord(String[] words) {
        Arrays.sort(words);
        Set<String> built = new HashSet<String>();
        String res = "";
        for (String word : words) {
            if (word.length() == 1 || built.contains(word.substring(0, word.length() - 1))) {
                res = res.length() < word.length() ? word : res;
                built.add(word);
            }
        }
        return res;
    }
}
</code></pre>

***
#### 解题思路
* 使用<code>Arrays.sort()</code>函数对字符串数组进行排序，所得到的新的字符串数组按照<font color = brown>字母表</font>以及<font color = brown>字典顺序</font>出现；
* 使用HashSet辅助，存下字典的可建set；
* 如果单词的长度增大，则更新返回单词。