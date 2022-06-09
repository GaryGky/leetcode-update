## Simple DP

The naive idea of Dynamic Programming is cache which means we have to break down the whole problem into several small problem. To find the solution for the big problem is to find the solution for sub problem. (找到最优子结构)。

As you may know that the critical point of DP problem is to find the recursion formular from which we can pile up the sub problem to the whole problem.



### [509. Fibonacci Number](https://leetcode.cn/problems/fibonacci-number/)

> One of the most classical problem in recursion and DP algorithm.

### Solution

The recursion formula is:
$$
dp[i] = dp[i-1] + dp[i-2]
$$
Because we only need to remember the last to dp value, we can optimize the array to two vars (a and b).

Each time we iterate i, we compute current fibo number based on a and b until reaching n.

```java
class Solution {
    public int fib(int n) {
        int a=0,b=1;
        if(n==0) return a;
        if(n==1) return b;
        for(int i=2;i<=n;i++){
            int tmp = a;
            a = b;
            b += tmp;
        }
        return b;
    }
}
```



### [70. Climbing Stairs](https://leetcode.cn/problems/climbing-stairs/)

### Solution

- Use DP Array to store the ways to climb to stair i.
- For each stair i, the ways to climb onto it equals to the ways to climb to i-1 plus ways to climb to i-2, because everytime we have choice for one step and two step.

```java
class Solution {
    public int climbStairs(int n) {
        if(n<=1) return 1;

        int[] dp = new int[n+1];
        dp[1] = dp[0] = 1;

        for(int i=2;i<=n;i++) dp[i] = dp[i-1] + dp[i-2];

        return dp[n];
    }
}
```



### [746. Min Cost Climbing Stairs](https://leetcode.cn/problems/min-cost-climbing-stairs/)

### Solution

- Use DP to store the minimum cost of reaching one level.

- And for each level (stair), we can have:
  $$
  dp[i] =\left\{
  \begin{aligned}
  & min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2]), i>1 \\
  & 0,i<=1 \\
  \end{aligned}
  \right.
  $$

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int[] dp = new int[n+1];
        for(int i=2;i<=n;i++){
            dp[i] = Math.min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2]);
        }
        return dp[n];
    }
}
```

