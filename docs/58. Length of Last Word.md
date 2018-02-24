## 58. Length of Last Word

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

**Note:** A word is defined as a character sequence consists of non-space characters only.

**Example:**

```
Input: "Hello World"
Output: 5
```

### Code:

```java
class Solution {
    public int lengthOfLastWord(String s) {
        String[] words = s.split(" ");
        if (words == null || words.length == 0) return 0;
        return words[words.length - 1].length();
    }
}
```

### 解题思路
* 先用split函数将字符串分割；
* 然后找到最后一个单词返回其长度。