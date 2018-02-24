## 345. Reverse Vowels of a String

Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**
Given s = "hello", return "holle".

**Example 2:**
Given s = "leetcode", return "leotcede".

**Note:**
The vowels does not include the letter "y".

### Code：

```java
class Solution {
    public String reverseVowels(String s) {
        if (s == null || s.length() == 0) return s;
        String vowels = "aeiouAEIOU";
        char[] chars = s.toCharArray();
        
        int left = 0, right = chars.length - 1;
        while (left < right) {
            while (left < right && !vowels.contains(chars[left] + "")) left++;
            while (left < right && !vowels.contains(chars[right] + "")) right--;
            
            char temp = chars[left];
            chars[left] = chars[right];
            chars[right] = temp;
            left++;
            right--;
        }
        return new String(chars);
    }
}
```

### 解题思路
* 使用首位指针法，循环条件是left < right;
* 内循环中，分别找到首、尾指针所指的元音字母；
* 再交换。