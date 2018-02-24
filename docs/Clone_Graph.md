## 133. Clone Graph

Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.


**OJ's undirected graph serialization:**
Nodes are labeled uniquely.

We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph {0,1,2#1,2#2,2}.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

1. First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
2. Second node is labeled as 1. Connect node 1 to node 2.
3. Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
Visually, the graph looks like the following:

```
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```

### Code:

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    Map<Integer, UndirectedGraphNode> map = new HashMap<Integer, UndirectedGraphNode>();
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        
        return clone(node);
    }
    
    public UndirectedGraphNode clone(UndirectedGraphNode node) {
        if (node == null) return null;
        if (map.containsKey(node.label)) {
            return map.get(node.label);
        }
        UndirectedGraphNode newNode = new UndirectedGraphNode(node.label);
        map.put(newNode.label, newNode);
        for (UndirectedGraphNode neighber : node.neighbors) {
            newNode.neighbors.add(clone(neighber));
        }
        return newNode;
    }
}
```

### 解题思路
* 使用递归函数clone，并且用HashMap辅助存储图中的节点；
* 在递归的过程中，如果元素存在于map中，则返回node；
* 对于node的所有neighbour递归。