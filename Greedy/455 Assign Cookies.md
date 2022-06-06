## [455. Assign Cookies](https://leetcode.cn/problems/assign-cookies/)

### Solution

- Can use Greedy Algorithm to solve the problem.
- Firstly, sort both g and s arrays.
- Then, both start from the beginning, trying to assign cookie j to child i
  - if successfully assigned, move to next child and cookie
  - otherwise, increase **Cookie** size (increase j)

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int i = 0, j = 0;
        int ans = 0;
        while(i < g.length && j < s.length){
            if(g[i] <= s[j]){
                i++;
                j++;
                ans++;
            }else {
                j++;
            }
        }
        return ans;
    }
}
```

