## 520. Detect Capital

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

* All letters in this word are capitals, like "USA".
* All letters in this word are not capitals, like "leetcode".
* Only the first letter in this word is capital if it has more than one letter, like "Google".
Otherwise, we define that this word doesn't use capitals in a right way.

**Example 1:**

```
Input: "USA"
Output: True
Example 2:
Input: "FlaG"
Output: False
```
**Note:** The input will be a non-empty word consisting of uppercase and lowercase latin letters.

### Code:

```java
class Solution {
    public boolean detectCapitalUse(String word) {
        String lowerCaseWord = word.toLowerCase();
        int difference = 0;
        for (int i = 0; i < word.length(); i++) {
            if (word.charAt(i) != lowerCaseWord.charAt(i)) difference += 1;
        }
        
        if (difference == 0 || difference == word.length()) return true;
        if (difference == 1 && word.charAt(0) != lowerCaseWord.charAt(0)) return true;
        return false;
    }
}
```
 
### 解题思路：
* 首先将字符串全部转换成小写，使用```word.toLowerCase();```
* 比较原字符串和新字符串的不一样的个数；
* 如果difference为0或word.length()，则返回真；
* 如果有且只有开头一个字符不等，也返回真；
* 其余情况返回假。
