## [332. Reconstruct Itinerary](https://leetcode.cn/problems/reconstruct-itinerary/)

### Solution

- To build a graph, use the representation method of a chain graph; each node is mapped to the nodes corresponding to all the outgoing edges of the node, and is sorted according to the lexicographical order.
- Implement `Hierholzer` algorithm to find **Euler Circle Path**.
- When Nodes still have edge to go, then recursively call DFS to dive into the path.
- Else add nodes to the list.
- Finally reverse the list and get the answer.

Time Complexity: O(E), E is the number of edges。

```java
class Solution {
    HashMap<String, PriorityQueue<String>> graph = new HashMap<>();
    LinkedList<String> ans = new LinkedList<>();
    public List<String> findItinerary(List<List<String>> tickets) {
        // buildgraph
        buildGraph(tickets);
        // dfs
        dfs("JFK");
        Collections.reverse(ans);
        return ans;
    }

    private void buildGraph(List<List<String>> tickets){
        for(List<String> ticket : tickets){
            String from = ticket.get(0), to = ticket.get(1);
            PriorityQueue<String> heap = graph.getOrDefault(from, new PriorityQueue<>());
            heap.offer(to);
            graph.put(from, heap);
        }
    }

    private void dfs(String from){
        while(graph.getOrDefault(from, new PriorityQueue<>()).size() > 0){
            dfs(graph.get(from).poll());
        }
        ans.addLast(from);
    }
}
```

