## 56. Merge Intervals

Given a collection of intervals, merge all overlapping intervals.

For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].

### Code

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> result = new ArrayList<Interval>();
        if (intervals.size() <= 1) return intervals;
        // 先根据每个interval的第一个元素将list初步排序
        Collections.sort(intervals, new Comparator<Object>() {
            public int compare(Object o1, Object o2) {
                Interval i1 = (Interval) o1;
                Interval i2 = (Interval) o2;
                if (i1.start > i2.start) return 1;
                else if (i1.start < i2.start) return -1;
                else return 0;
            }
        });
        
        int start = intervals.get(0).start;
        int end = intervals.get(0).end;
        // 对初排序的列表，根据第二个元素进行融合
        for (Interval interval : intervals) {
            if (interval.start <= end) // 如果发生覆盖
                end = Math.max(end, interval.end);
            else {                     // 如果不相交，将上一元素写入result，更新start与end
                result.add(new Interval(start, end));
                start = interval.start;
                end = interval.end;
            }
        }
    
        // Add the last interval
        result.add(new Interval(start, end));
        return result;
        }
}
```

### 解题思路：
* 首先根据每个间隔的第一个元素将列表排序（调用Collections的sort方法，使用compartor接口实现）；
* 然后判断第二个元素，如果发生覆盖现象，则更新end；
* 如果两个间隔不想交，则将间隔加入结果数组。