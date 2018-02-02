## 5. Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

**Example:**

```
Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
``` 

**Example:**

```
Input: "cbbd"

Output: "bb"
```
### Code:

```java
class Solution {
	private int lo, maxLen;
	public String longestPalindrome(String s) {  
		int len = s.length();
		if (len < 2) return s;
		
		for (int i = 0; i < len-1; i++) { //对于每一个字符，向两边扩展搜索是否为回文，更新起始位置和长度
			extendPalindrome(s, i, i);  //为奇数的情况
			extendPalindrome(s, i, i+1); //为偶数的情况
		}
		return s.substring(lo, lo+maxLen-1);
	}
	
	public extendPalindrome(String s, int j, int k) {
		while (j>=0 && s.charAt(j)==s.charAt(k)) {
			//此处找到当前字符能扩展的最长回文时，两边指针多移动了一位
			j--;  
			k++;
		}
		//如果长度大于maxLen，则更新两个全局变量
		if (maxLen < k-j-1) {
			lo = j + 1;
			maxLen = k-j-1;
		}
	}
}
```

### 解题思路
* 维护两个全局变量，lo是最长回文的最低位，maxLen是最长回文的长度；
* 在遍历字符串的每一位字符时，分长度为奇数或者偶数两种情况进行两边扩展搜索；
* 在每一个字符位搜索的时候更新最长回文的起始位置以及长度。