## 557. Reverse Words in a String III

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**

```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```
**Note:** In the string, each word is separated by single space and there will not be any extra space in the string.

### Code:

```java
class Solution {
    public String reverseWords(String s) {
        StringBuilder result = new StringBuilder();
        String[] words = s.trim().split(" ");
        
        for (int i = 0; i < words.length; i++) {
            StringBuilder temp = new StringBuilder(words[i]);
            result.append(temp.reverse());
            result.append(" ");
        }
        return result.toString().trim();
    }
}
```

### 解题思路：
* 使用split函数将字符串分割成单词；
* 再使用StringBuilder的reverse函数翻转单词内部的顺序；
* 最后拼接单词。