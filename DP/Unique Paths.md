## [62. Unique Paths](https://leetcode.cn/problems/unique-paths/)

### Solution

Initialize DP array to store the optimal solution for sub space. $$dp[i][j]$$ represents the unique path that can reach $$position[i][j]$$.

Because we know that one position can only be reach from the up and left position, we can make the transition formula as:
$$
dp[i][j]=\left\{
\begin{aligned}
& 1, i,j <= 1 \\
& dp[i-1][j] + dp[i][j-1], else
\end{aligned}
\right.
$$

```java
class Solution {
    public int uniquePaths(int m, int n) {
        // init
        int[][] dp = new int[m][n];
        dp[0][0] = 1;
        for(int i=0;i<m;i++) dp[i][0]=1;
        for(int i=0;i<n;i++) dp[0][i]=1;

        // DP Progress
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j] += dp[i-1][j] + dp[i][j-1];
            }
        }

        // for(int[] dpArr : dp) System.out.println(Arrays.toString(dpArr));

        return dp[m-1][n-1];
    }
}
```



## 63. [Unique Paths II](https://leetcode.cn/problems/unique-paths-ii/)

### Solution

Almost the same as unique path I. The only difference is that the position with obstacle is unreachable so that in DP array the position with obstacle should be 0, denotes unreachable status.

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        // can directly in-place DP
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        
        obstacleGrid[0][0] = obstacleGrid[0][0]==1 ? 0 : 1;

        for(int i=1;i<m;i++) obstacleGrid[i][0] = obstacleGrid[i][0]==1 ? 0 : obstacleGrid[i-1][0];
        if(n==1) return obstacleGrid[m-1][0];

        for(int j=1;j<n;j++) obstacleGrid[0][j] = obstacleGrid[0][j]==1 ? 0 : obstacleGrid[0][j-1];

        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(obstacleGrid[i][j] == 1) {
                    obstacleGrid[i][j] = 0;
                    continue;
                }
                obstacleGrid[i][j] += obstacleGrid[i-1][j] + obstacleGrid[i][j-1];
            }
        }

        return obstacleGrid[m-1][n-1];
    }
}
```

