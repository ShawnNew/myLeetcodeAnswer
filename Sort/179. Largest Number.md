## 179. Largest Number

Given a list of non negative integers, arrange them such that they form the largest number.

For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.

### Code

```java
class Solution {
    public String largestNumber(int[] nums) {
        if (nums.length == 0 || nums == null) return "";
        
        String[] numsString = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            numsString[i] = String.valueOf(nums[i]);
        }
        
        Comparator<String> comp = new Comparator<String>() {
            @Override
            public int compare(String str1, String str2) {
                String s1 = str1 + str2;
                String s2 = str2 + str1;
                return s2.compareTo(s1);   //交换s1与s2，降序排列
            }
        };
        
        Arrays.sort(numsString, comp);
        if (numsString[0].charAt(0) == '0') return "0";
        
        StringBuilder sb = new StringBuilder();
        for (String str : numsString) {
            sb.append(str);
        }
        return sb.toString();
    }
}
```


### 解题思路

* 将数组转换成字符串数组；
* 拼接两个元素，比较str1+str2与str2+str1的大小；
* 使用Arrays.sort调用comparator接口；
* 在comparator接口中判断str1+str2与str2+str1，降序排序；
* 然后使用append将元素加入新的字符串中并返回。