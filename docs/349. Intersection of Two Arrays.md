## Intersection of Two Arrays
Given two arrays, write a function to compute their intersection.</br>

<strong>Example:</strong></br>
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].</br>

<strong>Note:</strong></br>

* Each element in the result must be unique.
* The result can be in any order.

### Code:
<pre><code>
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set< Integer > hs1 = new HashSet< Integer >();
        Set< Integer > hs2 = new HashSet< Integer >();
        
        if (nums1 == null || nums2 == null) return null;  //判断特殊情况
        
        for (int i = 0; i < nums1.length; i++) {   //遍历nums1，找到不重复的元素
            if (!hs1.contains(nums1[i])) hs1.add(nums1[i]);
        }
        
        List< Integer > list = new ArrayList< Integer >();
        for (int j = 0; j < nums2.length; j++) {   //遍历nums2，找到交集
            if (!hs2.contains(nums2[j]) && hs1.contains(nums2[j])) {
                list.add(nums2[j]);
                hs2.add(nums2[j]);
            }
        }
        int[] res = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {  //返回结果
            res[i] = list.get(i);
        }
        return res;
    }
}
</code></pre>

***
* 该题的解题思路是考虑使用相同元素的Hash值相同的特点，使用HashSet来找到数组中的不同元素；
* 先遍历其中一个数组，找到不重复的元素；
* 再遍历另外一个数组，找到两数组中的交集，并将交集元素存入ArrayList中（此处运用了ArrayList的可变长的特点）；
* 最后将ArrayList转换为整型数组。
