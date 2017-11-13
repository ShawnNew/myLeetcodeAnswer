## K-diff Pairs in an Array

Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.

<pre><code>
class Solution {
    public int findPairs(int[] nums, int k) {
        
        if (nums == null || nums.length == 0 || k < 0) { //特殊情况：数组为空或者长度为零
            return 0;
        }
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();   //定义HashMap，将数组的元素存入其中
        
        int res = 0;
        for (int i = 0; i < nums.length; i++) {  //存数
            map.put(nums[i], i);
        }
        for (int i = 0; i < nums.length; i++) {  //找到满足条件的元素，返回值加一
            if (map.containsKey(nums[i] + k) && map.get(nums[i] + k) != i) {  
                map.remove(nums[i] + k);  
                res++;  
            }  
        }
        
        return res;
    }
}
</code></pre>

***
* 该问题以固定一种情形的思路求解
* 先将数组元素放入HashMap中，key存元素的值，value存入元素的索引。
* 再对数组遍历一遍，找到当前元素满足<code>nums[i]+k</code>的元素，并且删除找到的元素，计数器加一。

***
### <em>用entry遍历HashMap的解法</em>

<pre><code>
class Solution {
	public int findPairs (int[] nums, int k) {
		HashMap<Integer, Integer> map = new HashMap<Integer, Integer>(); //定义HashMap
		int res = 0;          //定义返回值
		for (int e : nums) {  //将数组存入HashMap
			map.put(e, map.getOrDefault(e, 0) + 1);	
		}
		for (Map.Entry<Integer, Integer> entries : map.entrySet()) {            //用entry来循环HashMap
			if (k == 0) {               //k为零时，如果元素重复次数大于等于2，则计数器加一
				if (entries.getValue() >= 2) {
					res++;
				}
			} else {                    //k不为零，则查找entry下HashMap中是否有满足条件的元素存在
				if (map.containsKey(entries.getKey() + k)) {
					res++;
				}
			}
		}
		return res;
	}
}
</code></pre>

***
* 该解法使用HashMap的entry来遍历。
* 注意entries.getKey()方法返回一个和entries对应的key，for(Map.Entry entries)执行循环。