## 30. Substring with Concatenation of All Words

You are given a string, **s**, and a list of **words**, **words**, that are all of the same length. Find all starting indices of substring(s) in **s** that is a concatenation of each word in words exactly once and without any intervening characters.

For example, given:
**s**: "barfoothefoobarman"
**words**: ["foo", "bar"]

You should return the indices: [0,9].
(order does not matter).

### Code

```java
class Solution {
    /*
    The problem can be solved using HashMap, by count the occurance of word
    in words array.
    When looping s, check every word of existance at such position.
    */
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<Integer>();
        if (s == null || words == null || words.length == 0) return res;
        int wordLen = words[0].length();
        int numWords = words.length;
        
        Map<String, Integer> map = new HashMap<String, Integer>();
        for (String str : words) map.put(str, map.getOrDefault(str, 0) + 1); // count the occurance of words
        
        for (int i = 0; i <= s.length() - wordLen * numWords; i++) { 
            // loop every position of string to find a match
            Map<String, Integer> copy = new HashMap<String, Integer>(map);
            for (int j = 0; j < numWords; j++) {  
                // find if the words match
                String word = s.substring(i + j*wordLen, i + wordLen*j + wordLen); // get the word
                
                if (copy.containsKey(word)) {  // if the word remains in the hashmap
                    int count = copy.get(word);
                    // delete the key-value set or count-1
                    if (count == 1) {
                        copy.remove(word);
                    } else {
                        copy.put(word, count - 1);
                    }
                    
                    // add the index into the list if hashmap is empty
                    if (copy.isEmpty()) {
                        res.add(i);
                        break;
                    }
                } else 
                    break;
            }
        }
        
        return res;
    }
}
```

### 解题思路
* 使用HashMap辅助解题，HashMap中的key-value分别存如下信息：
	* key : word
	* value : 在words数组中每一个词出现的次数
* 遍历字符串s，在每一位字符（不超过索引）上判断words的长度是否匹配，检查后面的wordLen*numWords范围内是否存在匹配；
* 在遍历的过程中对于每一个子字符串所构成的单词，查找其在HashMap中是否存在，并对其在HashMap中进行删除或者count-1操作；
* 如果出现HashMap为空的情况，则可以将位置索引加入结果的list中。