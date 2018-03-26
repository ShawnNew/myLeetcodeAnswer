## 215. Kth Largest Element in an Array

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,

Given [3,2,1,5,6,4] and k = 2, return 5.

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length.

### 方法一（PriorityQueue）

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Queue<Integer> queue = new PriorityQueue<Integer>(nums.length, new Comparator<Integer>() {
           @Override
            public int compare(Integer o1, Integer o2) {
                return o2 - o1;
            }
        });
        
        for (int i : nums) {
            queue.offer(i);
        }
        
        for (int i = 0; i < k-1; i++) {
            queue.poll();
        }
        
        return queue.peek();
    }
}
```

借助PriorityQueue，将数组中的元素按顺序放入队列，再查看第k个元素即可。

### 方法二(quickselect)

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        int pos = partition(nums, 0, len-1, len-k+1);
        return nums[pos];
    }
    
    // return the kth smallest element
    public int partition(int[] nums, int start, int end, int k) {
        int pivot = nums[end];
        int tail = start - 1;  // the tail of the small subset
        for (int i = start; i < end; i++) {
            if (nums[i] <= pivot) swap(nums, ++tail, i);
        }
        swap(nums, ++tail, end);  // tail is the pivot position here
        
        // count the numbers that <= pivot
        int m = tail - start + 1;
        if (m == k) return tail;  // pivot is the kth smallest element
        // pivot is large, then the kth smallest must be in the left part
        else if (m > k) return partition(nums, start, tail-1, k);
        // pivot is small, then the kth smallest must be in the right part
        else return partition(nums, tail+1, end, k-m);
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

* 可以使用quicksort的思路解题，找到中轴元素，将较小和较大的元素分区；
* 找到数组中第len-k+1个最小的元素，这个元素即为第k个最大的元素；
* 比较pivot前面的元素个数m与k的大小，如果```m==k```则说明中轴元素为kth smallest；
* 如果```m>k```，说明中轴元素大，kth smallest在左半部分；
* 如果```m<k```，说明中轴元素小，kth smallest在右半部分。