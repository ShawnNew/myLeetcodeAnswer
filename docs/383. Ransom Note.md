## 383. Ransom Note
Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

**Note:**
You may assume that both strings contain only lowercase letters.

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

### Code:

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] chars = new int[26];
        for (char c : ransomNote.toCharArray()) chars[c - 'a']++;
        for (char c : magazine.toCharArray()) chars[c - 'a']--;
        for (int i = 0; i < chars.length; i++) {
            if (chars[i] > 0) return false;
        }
        return true;
    }
}
```

### 解题思路：
* 用26位整型数组分别记录26个英文字母出现的次数；
* 遍历ransomNote字符串，出现次数递增；
* 遍历magazine字符串，出现次数递减；
* 整型数组中如果有元素大于零，则返回false。