### Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

<pre><code>
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        //定义三个指针，分别指向两个数组和新生成的数组
        int id1 = m - 1;
        int id2 = n - 1;
        int count = m + n - 1;
        while (id1 >= 0 || id2 >= 0) {
            if (id1 < 0) {
                nums1[count--] = nums2[id2--];
            } else if (id2 < 0) {
                nums1[count--] = nums1[id1--];
            } else {
                nums1[count--] = nums1[id1] > nums2[id2] ? nums1[id1--] : nums2[id2--];             
            }            
        }
    }
}
</code></pre>
* 因为两个数组都是已排序的数组，并且<code>nums1</code>空间足够，所以只要考虑将<code>nums2</code>加入到<code>nums1</code>就可以。
* 从<code>nums1</code>数组的最后一位开始加入元素，比较<code>nums1</code>和<code>nums2</code>的当前位大小，较大元素放入新数组中。
* <code>nums1</code>和<code>nums2</code>中谁的索引小于零，则把另外一个数组的元素加入到新数组后面即可。