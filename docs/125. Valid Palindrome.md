## 125. Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

**Note:**

Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

### Code:
```java
class Solution {
    public boolean isPalindrome(String s) {
        s = s.replaceAll("[\\W]", "");   // "[\\W]"是正则表达式，表示非字母数字的字符
        s = s.toLowerCase();
        
        if (s.length() == 0) return true;
        int start = 0, end = s.length() - 1;
        while (start < end) {        //循环条件是start < end，注意不是start != end
            if (s.charAt(start) != s.charAt(end)) return false;
            start++; end--;
        }
        return true;
    }
} 
```

### 解题思路
* 本题考虑使用String类中的replaceAll函数配合正则表达式将字符串中的非字母数字字符替换掉；
* 在使用String类中的toLowerCase函数将字符串中的所有字符都变换成小写；
* 最后使用双指针法遍历字符串。

### Improvement:
```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s.length() == 0) return true;
        char cStart, cEnd;
        int start = 0, end = s.length() - 1;
        while (start <= end) {        //循环条件是start <= end，注意不是start != end
            cStart = s.charAt(start);
            cEnd = s.charAt(end);
            if (!Character.isLetterOrDigit(cStart)) {
                start++;
            } else if (!Character.isLetterOrDigit(cEnd)) {
                end--;
            } else {
                if (Character.toLowerCase(cStart) != Character.toLowerCase(cEnd)) return false;
                start++; end--;
            }
        }
        return true;
    }
}
```
### 改进版解题思路
* 不用首先使用replaceAll和toLowerCase，会增加复杂度；
* 直接遍历一遍字符串，使用Character类中的isLetterorDigit和toLowerCase方法即可完成。