## House Robber

### [198. House Robber](https://leetcode.cn/problems/house-robber/)

- dp[i] denotes that robbering house[i] can benefit the maximum value.

```java
class Solution {
    public int rob(int[] nums) {
        int rst = 0;
        int n = nums.length;
        int[] dp = new int[n];
        for(int i=0;i<n;i++){
            int max = nums[i];
            for(int j=i-2;j>=0;j--){
                max = Math.max(dp[j] + nums[i], max);
            }
            dp[i] = max;
            rst = Math.max(rst, max);
        }
        return rst;
    }
}
```

### [213. House Robber II](https://leetcode.cn/problems/house-robber-ii/)

The difference between II and I is that the first and the last house cannot be robbed at the same time. So I divide the scenario into two kind:

- On the first one, the robber can rob the first house but not the last.
- On the other one, the robeber can rob the last house but not the first.

Then, get the max value of two kind.

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1) return nums[0];

        int start = robHelper(Arrays.copyOfRange(nums, 0, nums.length-1));
        int end = robHelper(Arrays.copyOfRange(nums, 1, nums.length));

        return start>end?start:end;
    }

    private int robHelper(int[] nums){
        int[] maxRobbing = new int[nums.length];
        int res = 0;

        for(int i=0;i<nums.length;i++){
            if(i<=1) maxRobbing[i]=nums[i];
            else {
                int tmp = maxRobbing[i-1];
                for(int j=i-2;j>=0;j--){
                    tmp = tmp>(maxRobbing[j] + nums[i])?tmp:(maxRobbing[j] + nums[i]);
                }
                maxRobbing[i] = tmp;
            }

            res = res>maxRobbing[i]?res:maxRobbing[i];
        }

        return res;
    }
}
```

### [337. House Robber III](https://leetcode.cn/problems/house-robber-iii/)

DFS with two different situation:

- Rob current node: then can only rob the current node's children's children.
- Not Rob current node: then can rob the current node's children.

```java
class Solution {
    HashMap<TreeNode, Integer> mem;
    public int rob(TreeNode root) {
        mem = new HashMap<>();
        return dfs(root);
    }

    private int dfs(TreeNode root){
        if(root == null) return 0;
        if(mem.containsKey(root)) return mem.get(root);

        // dont rob current node
        int valNonCurrentNode = dfs(root.left) + dfs(root.right);
        // rob current node
        int valRobCurrentNode = 0;
        if(root.left != null) valRobCurrentNode += dfs(root.left.left) + dfs(root.left.right);
        if(root.right != null) valRobCurrentNode += dfs(root.right.right) + dfs(root.right.left);

        int rst = Math.max(root.val + valRobCurrentNode, valNonCurrentNode);
        mem.put(root, rst);
        return rst;
    }
}
```

