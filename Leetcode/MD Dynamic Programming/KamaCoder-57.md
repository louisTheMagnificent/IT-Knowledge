## Question: 

https://kamacoder.com/problempage.php?pid=1067

---
## Thought:
We use md dp to do it but only 1d array.

https://programmercarl.com/0070.爬楼梯完全背包版本.html#思路

---
## Solution:
```Java
import java.util.Scanner;
public class Main{
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int m, n;
        m = scan.nextInt();
        n = scan.nextInt();
        
        int[] dp = new int[m + 1];
        dp[0] = 1;
        
        for(int j = 1; j <= m; j++){
            for(int i = 1; i <= n; i++){
                if(j >= i) dp[j] += dp[j - i];
            }
        }
        
        scan.close();
        System.out.println(dp[m]);
    }
}
```
Time complexity: O(mn)  
Space complexity: O(n)
