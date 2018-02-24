## Intersection of Two Arrays II
Given two arrays, write a function to compute their intersection.</br>

<strong>Example:</strong></br>
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].</br>

<strong>Note:</strong></br>

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

### Code:
<pre><code>
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);  //先对数组排序
        Arrays.sort(nums2);
        
        int pointer1 = 0, pointer2 = 0;
        int len1 = nums1.length, len2 = nums2.length;
        List<Integer> list = new ArrayList<Integer>();
        
        while (pointer1 < len1 && pointer2 < len2) { //用双指针遍历
            if (nums1[pointer1] > nums2[pointer2]) { //对于已排序的数组，只需比较值的大小，再移动指针即可
                pointer2++;
            } else if (nums1[pointer1] < nums2[pointer2]) {
                pointer1++;
            } else {
                list.add(nums1[pointer1]);
                pointer1++; pointer2++;
            }
        }
        
        int[] res = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {  //返回输出值
            res[i] = list.get(i);
        }
        return res;
    }
}
</code></pre>

***
* 该题的解题思路是先对数组进行排序，然后使用双指针找到交集。
* 对于已经排序的数组，比较指针所指向元素的大小，分别移动指针；
* 如果相等则可以记录相等元素。