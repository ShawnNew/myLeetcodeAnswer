## 278. First Bad Version

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

### Code:

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
    int start = 1, end = n;
    while (start < end) {
        int mid = (start + end) >>> 1;
        if (!isBadVersion(mid)) start = mid + 1;
        else end = mid;            
    }        
    return start;
    }
}
```
### 解题思路
* 使用二分查找解决此题。