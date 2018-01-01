## 606. Construct String from Binary Tree

You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.

The null node needs to be represented by empty parenthesis pair "()". And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.

**Example 1:**

```
Input: Binary tree: [1,2,3,4]
       1
     /   \
    2     3
   /    
  4     

Output: "1(2(4))(3)"

Explanation: Originallay it needs to be "1(2(4)())(3()())", 
but you need to omit all the unnecessary empty parenthesis pairs. 
And it will be "1(2(4))(3)".
```
**Example 2:**

```
Input: Binary tree: [1,2,3,null,4]
       1
     /   \
    2     3
     \  
      4 

Output: "1(2()(4))(3)"

Explanation: Almost the same as the first example, 
except we can't omit the first parenthesis pair to break the one-to-one mapping relationship between the input and the output.
```

### Code:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public String tree2str(TreeNode t) {
        StringBuilder sb = new StringBuilder();
        //helper(t);
        return sb.append(helper(t)).toString();
    }
    public String helper(TreeNode t){
        if (t == null) return "";
        StringBuilder sb = new StringBuilder();
        if(t!=null){
            sb.append(t.val);
            if(t.left!=null||t.right!=null){
                sb.append("(");
                sb.append(helper(t.left));
                sb.append(")");
                if(t.right!=null){
                    sb.append("(");
                    sb.append(helper(t.right));
                    sb.append(")");
                }
            }
        }
        return sb.toString();
    }
}
```

### 解题思路：
* 使用helper函数实现递归；
* 递归的基本条件是当前结点为空，返回空字符串```return "";```
* 递归式要分情况讨论，如果两边都空，则只加上```sb.append(t.val);```
* 如果左边不为空只加上```"(t.left)"```；
* 如果右边不为空则加上```"()(t.right)"```。