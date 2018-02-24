## 734. Sentence Similarity
Given two sentences words1, words2 (each represented as an array of strings), and a list of similar word pairs pairs, determine if two sentences are similar.

For example, "great acting skills" and "fine drama talent" are similar, if the similar word pairs are pairs = [["great", "fine"], ["acting","drama"], ["skills","talent"]].

Note that the similarity relation is not transitive. For example, if "great" and "fine" are similar, and "fine" and "good" are similar, "great" and "good" are not necessarily similar.

However, similarity is symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences words1 = ["great"], words2 = ["great"], pairs = [] are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like words1 = ["great"] can never be similar to words2 = ["doubleplus","good"].


### Code:
<pre><code>class Solution {
    public boolean areSentencesSimilar(String[] words1, String[] words2, String[][] pairs) {
        if (words1.length != words2.length) return false;
        
        Map<String, Set<String>> map = new HashMap<>();
        
        for (String[] pair : pairs) {
            if (!map.containsKey(pair[0])) map.put(pair[0], new HashSet<>());
            map.get(pair[0]).add(pair[1]);
        }
        
        for (int i = 0; i < words1.length; i++) {
            if (!words1[i].equals(words2[i]) && !map.getOrDefault(words1[i], new HashSet<>()).contains(words2[i]) && !map.getOrDefault(words2[i], new HashSet<>()).contains(words1[i])) return false;
        }
        return true;
    }
}
</code></pre>

***
#### 解题思路
* 使用HashMap存储pairs，遍历字符串数组，找到不满足条件的则返回false。