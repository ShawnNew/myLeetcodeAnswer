## Find All Anagrams in a String

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

<strong>Example 1:</strong>
<pre><code>
<strong>Input:</strong>
s: "cbaebabacd" p: "abc"</br>
<strong>Output:</strong>
[0, 6]</br>
<strong>Explanation:</strong>
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
</code></pre>
<strong>Example 2:</strong>
<pre><code>
<strong>Input:</strong>
s: "abab" p: "ab"</br>
<strong>Output:</strong>
[0, 1, 2]</br>
<strong>Explanation:</strong>
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
</code></pre>

### Code:
<pre><code>
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        Map< Character, Integer> map = new HashMap< Character, Integer>();
        List< Integer> res = new ArrayList<Integer>();
        char[] pArray = p.toCharArray();
        
        if (s == null || p == null || s.length() == 0 || p.length() == 0) return res;
        
        for (char c : pArray) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        
        int right = 0, left = 0, counter = map.size();
        while (right < s.length()) {
            char c = s.charAt(right);
            if (map.containsKey(c)) {
                map.put(c, map.get(c) - 1);
                if (map.get(c) == 0) counter--;  //右边窗口排除一个有用字符，counter--
            }
            right++;   //还有需要查找的有用字符，移动右端窗口
            
            while (counter == 0) {  //有用字符长度为0，则移动左端窗口
                char temp = s.charAt(left);
                if (map.containsKey(temp)) {
                    map.put(temp, map.get(temp) + 1);
                    if (map.get(temp) > 0) counter++;  //左边窗口增加一个有用字符，counter++
                }
                if (right - left == p.length()) res.add(left);
                left++;
            }
        }
        return res;
    }
}
</code></pre>

***
* 先用HashMap对p字符串进行记录，将出现次数存入value中；
* 在遍历s字符串的过程中，使用滑动窗口；
* 移动窗口右边界，找到HashMap中的元素，将频数减一，如果频数降为零，counter减一；
* counter为零时移动左边窗口，如果元素出现在HashMap中，增加频数，如果频数大于零，则counter加一；
* 如果窗口长度等于p的长度，则输出一个满足条件的结果。