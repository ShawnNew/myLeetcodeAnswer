## 784. Letter Case Permutation

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.  Return a list of all possible strings we could create.

```
Examples:
Input: S = "a1b2"
Output: ["a1b2", "a1B2", "A1b2", "A1B2"]

Input: S = "3z4"
Output: ["3z4", "3Z4"]

Input: S = "12345"
Output: ["12345"]
```

**Note:**

* S will be a string with length at most 12.
* S will consist only of letters or digits.

### Code

```java
class Solution {
    public static List<String> letterCasePermutation(String S) {
        char[] chars = S.toLowerCase().toCharArray();
        List<String> result = new ArrayList<String>();
        return helper(chars, 0, "", result); //从空字符串开始一位一位添加
    }
    
    public static List<String> helper(char[] chars, int index, String s, List<String> list) {
        if (index >= chars.length) {
            list.add(s);
        } else {
            char lower = chars[index];
            char upper = Character.toUpperCase(lower);
            //递归调用
            list = helper(chars, index+1, s+lower, list); //加入小写字母
            if (lower != upper) { //加入大写字母
                list = helper(chars, index+1, s+upper, list);
            }
        } 
        return list;
    } 
}
```

### 解题思路

* 从空字符串开始，一位一位开始添加字符，递归生成字符串；
* base case是当前遍历的位置索引超出字符数组的长度，则将字符串加入结果list；
* 递归式是每一位可以加入*大写字母*和*小写字母*两种情况。