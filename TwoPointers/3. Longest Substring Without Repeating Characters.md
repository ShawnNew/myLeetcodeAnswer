## 3. Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

**Examples:**

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int fast = 0, slow = 0;
        int len = 0;
        Set<Character> set = new HashSet<Character>();
        
        while (fast < s.length()) {
            if (!set.contains(s.charAt(fast))) {
                set.add(s.charAt(fast++));
                len = Math.max(len, set.size());
            } else {
                set.remove(s.charAt(slow++));
            }
        }
        return len;
    }
}
```

### 解题思路
* 使用HashSet辅助存储所有不重复的元素；
* 使用快慢指针，快指针遍历数组，同时更新len的长度；
* 当快指针出现重复时，移动慢指针，知道快指针不重复为止。