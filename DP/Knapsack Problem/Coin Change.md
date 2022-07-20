### Coin Change

#### [518. Coin Change 2](https://leetcode.cn/problems/coin-change-2/)

完全背包 × 组合问题

```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount+1];
        dp[0]=1;
        for(int coin : coins){
            for(int i=coin;i<=amount;i++){
                dp[i] += dp[i-coin];
            }
        }
        return dp[amount];
    }
}
```

#### [322. Coin Change](https://leetcode.cn/problems/coin-change/)

完全背包 × 最值问题

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        // OutLoop: Item
        // InnerLoop: Pack
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, Integer.MAX_VALUE / 2);
        dp[0] = 0;

        for(int coin : coins){
            for(int i=coin;i<=amount;i++){
                dp[i] = Math.min(dp[i], dp[i-coin]+1);
            }
        }

        return dp[amount]==Integer.MAX_VALUE / 2? -1 : dp[amount];
    }
}
```

#### [279. Perfect Squares](https://leetcode.cn/problems/perfect-squares/)

完全背包 × 最值问题

> Here the **items** are square number set less than n.

```java
class Solution {
    private ArrayList<Integer> item;
    public int numSquares(int n) {
        genItemBaseOnTarget(n);
        int[] dp = new int[n+1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for(Integer item : item){
            for(int i=item;i<=n;i++){
                dp[i] = Math.min(dp[i], dp[i-item] + 1);
            }
        }

        return dp[n];
    }

    private void genItemBaseOnTarget(int n){
        item = new ArrayList<>();
        for(int i=1;i * i<=n;i++){
            item.add(i * i);
        }
    }
}
```

