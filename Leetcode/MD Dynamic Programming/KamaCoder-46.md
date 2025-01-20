## Question:

https://kamacoder.com/problempage.php?pid=1046

---
## Thought:
We use md dp to do it.

https://programmercarl.com/背包理论基础01背包-1.html#思路

---
## Solution:
```Java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int bagweight = scanner.nextInt();

        int[] weight = new int[n];
        int[] value = new int[n];

        for (int i = 0; i < n; ++i) {
            weight[i] = scanner.nextInt();
        }
        for (int j = 0; j < n; ++j) {
            value[j] = scanner.nextInt();
        }
        
        int[][] dp = new int[n][bagweight + 1];
        
        for(int j = 1; j < bagweight + 1; j++){
            if(j < weight[0]){
                dp[0][j] = dp[0][j - 1];
            }
            else{
                dp[0][j] = value[0];
            }
        }
        
        for(int i = 1; i < n; i++){
            for(int j = 0; j < bagweight + 1; j++){
                if(j < weight[i]){
                    dp[i][j] = dp[i - 1][j];
                }
                else{
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);
                }
            }
        }
        System.out.println(dp[n - 1][bagweight]);
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
