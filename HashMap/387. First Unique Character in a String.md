## First Unique Character in a String
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

<strong>Examples:</strong>
<pre><code>
s = "leetcode"
return 0.
s = "loveleetcode",
return 2.
</code></pre>

<strong>Note:</strong>You may assume the string contain only lowercase letters.

### Original Code:
<pre><code>
class Solution {
    public int firstUniqChar(String s) {
        Map<Character, Integer[]> hm = new HashMap<Character, Integer[]>();
        int len = s.length();
        
        //遍历字符串，记录字符为key，保存其索引值和个数值为value
        for (int i = 0; i < len; i++) {
            char c = s.charAt(i);
            if (!hm.containsKey(c)) {
                hm.put(c, new Integer[]{i, 1});
            } else {
                Integer[] value = hm.get(c);
                value[0] = i;
                value[1] += 1;
                hm.put(c, value);
            }
        }
        
        //遍历HashMap，返回结果
        int res = len - 1;
        int uniqueCounter = 0;
        for (Map.Entry<Character, Integer[]> entry : hm.entrySet()) {
            Integer[] value = entry.getValue();    
            if (value[1] == 1) {
                uniqueCounter++;
                res = res < value[0] ? res : value[0];
            }
        }
        if (uniqueCounter == 0) return -1;
        return res;
    }
}
</code></pre>

***
* 解题思路是遍历字符串，使用HashMap存下每个字符，并且记录其索引值和出现的个数；
* 最后遍历一遍HashMap，找到索引值最小的并且出现个数为1的元素输出。

### 改进算法（256位数组）
<pre><code>
public class Solution {
    public int firstUniqChar(String s) {
        int freq [] = new int[256];
        
        //遍历一遍字符串，记录每个字符出现的频率
        for(int i = 0; i < s.length(); i++) {
            freq [s.charAt(i) - 'a']++;
        }
        
        //再遍历一遍字符串，在第一个unique字符处输出1
        for(int i = 0; i < s.length(); i++) {
            if(freq [s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }
        return -1;
    }
}
</code></pre>

***
* 改进算法的test cases的runtime比original算法要小很多，此处注意讨论遍历HashMap的速度的问题。

