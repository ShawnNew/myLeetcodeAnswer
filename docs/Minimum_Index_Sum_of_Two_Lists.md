## 599. Minimum Index Sum of Two Lists
Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.</br>
<strong>Example1:</strong>
<pre>Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".</pre>
<strong>Example2:</strong>
<pre>Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).</pre>
<strong>Note:</strong>

1. The length of both lists will be in the range of [1, 1000].
2. The length of strings in both lists will be in the range of [1, 30].
3. The index is starting from 0 to the list length minus 1.
4. No duplicates in both lists.

### Code:
<pre><code>class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        Map<String, Integer> map = new HashMap<String, Integer>();
        int minIndex = Integer.MAX_VALUE;
        List<String> res = new ArrayList<String>();
        for (int i = 0; i < list1.length; i++) map.put(list1[i], i);
        for (int i = 0; i < list2.length; i++) {
            Integer j = map.get(list2[i]);
            if (j != null && i + j <= minIndex) {
                if (i + j < minIndex) {
                    res.clear();
                    minIndex = i + j;
                }
                res.add(list2[i]);
            }   
        }
        return res.toArray(new String[res.size()]);
    }
}
</code></pre>

***
* 使用HashMap和ArrayList辅助；
* HashMap记录第一个字符串数组中的字符串和索引值；
* 遍历第二个字符串数组，如果索引值之和在变小，则清空列表和更改最小索引值，再加入新的列表；
* 如果索引值之和保持不变，则直接加入新的字符串。