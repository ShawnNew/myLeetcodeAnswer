## 75. Sort Colors

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:**
You are not suppose to use the library's sort function for this problem.

### 快速排序 O(nlogn)

```java
class Solution {
    public void swap(int[] nums, int i, int j) {   //交换两个元素
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public int partition (int[] nums, int left, int right) {  //将小于pivot元素都放在左边，大于pivot的元素都放在右边
        int pivot = nums[right];
        int tail = left - 1;
        
        for (int i = 0; i < right; i++) {
            if (nums[i] <= pivot) swap(nums, ++tail, i);
        }
        swap(nums, tail+1, right);
        return tail+1;
    }
    
    public void quickSort(int[] nums, int left, int right) {  //递归使用快速排序
        if (left >= right) return;
        int pivot_index = partition(nums, 0, right);
        quickSort(nums, 0, pivot_index-1);
        quickSort(nums, pivot_index+1, right);
    }
    
    public void sortColors(int[] nums) {
        int len = nums.length;
        quickSort(nums, 0, len-1);  //调用快排
    }
}
```

### 冒泡排序 O(n^2)

```java
class Solution {
    public void swap(int[] nums, int i, int j) {   //交换两个元素
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public void bubbleSort(int[] nums, int n) {
        for (int i=0; i < n-1; i++) {
            for (int j = 0; j < n-i-1; j++) {
                if (nums[j] > nums[j+1]) swap(nums, j, j+1);
            }
        }
    }
    
    public void sortColors(int[] nums) {
        int len = nums.length;
        bubbleSort(nums, len);  //调用冒泡排序
    }
}
```

### 选择排序 O(n^2)

```java
class Solution {
    public void swap(int[] nums, int i, int j) {   //交换两个元素
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public void selectSort(int[] nums, int n) {
        for (int i = 0; i < n-1; i++) {
            int min = nums[i];
            for (int j = i+1; j < n; j++) {
                if (nums[j] < min) {
                    min = nums[j];
                    swap(nums, j, i);
                }
            }
        }
    }
    
    public void sortColors(int[] nums) {
        int len = nums.length;
        selectSort(nums, len);  //调用选择排序
    }
}
```

### 插入排序 O(n^2)

```java
class Solution {
    public void insertSort(int[] nums, int n) {
        for (int i = 1; i < n; i++) {
            int get = nums[i];
            int j = i-1;
            while (j >= 0 && nums[j] > get) {
                nums[j+1] = nums[j]; 
                j--;
            }
            nums[j+1] = get;
        }
    }
    
    public void sortColors(int[] nums) {
        int len = nums.length;
        insertSort(nums, len);  //调用选择排序
    }
}
```