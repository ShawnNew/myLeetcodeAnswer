## 49. Group Anagrams

Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
Return:

```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:** All inputs will be in lower-case.

### Code:

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> hm = new HashMap<String, List<String>>();
        
        for (String s : strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String newString = new String(chars);
            
            if (!hm.containsKey(newString)) {
                List<String> tempList = new ArrayList<String>();
                tempList.add(s);
                hm.put(newString, tempList);
            } else hm.get(newString).add(s);
        }
        
        List<List<String>> result = new ArrayList<List<String>>();
        for (String str : hm.keySet()) {
            result.add(hm.get(str));
        }
        
        return result;
    }
}
```

### 解题思路
* 使用Hashmap辅助遍历字符串数组，对于每一个字符串，将其排序后取hash值，如果是anagram，则排序后的hash值相等。
* 如果不存在排序后的字符串，则放入hashmap，否则将当前遍历字符串加入List中。
* 遍历完字符串数组后，对于hashmap遍历，将value存入result数组。