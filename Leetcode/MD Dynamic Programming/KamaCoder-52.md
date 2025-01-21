## Question:

https://kamacoder.com/problempage.php?pid=1052

---
## Thought 1:
We use md dp to do it.

https://programmercarl.com/背包问题理论基础完全背包.html

---
## Solution 1:
```Java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int bagWeight = scanner.nextInt();

        int[] weight = new int[n];
        int[] value = new int[n];

        for (int i = 0; i < n; i++) {
            weight[i] = scanner.nextInt();
            value[i] = scanner.nextInt();
        }

        int[][] dp = new int[n][bagWeight + 1];

        for(int j = weight[0]; j <= bagWeight; j++){
            dp[0][j] = dp[0][j - weight[0]] + value[0];
        }
        
        for(int i = 1; i < n; i++){
            for(int j = 0; j <= bagWeight; j++){
                if (j < weight[i]) {
                    dp[i][j] = dp[i - 1][j];
                }
                else dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - weight[i]] + value[i]);
            }
        }

        System.out.println(dp[n - 1][bagWeight]);
        scanner.close();
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)

---
## Thought 2:
We use md dp to do it but only 1d array.

https://programmercarl.com/背包问题完全背包一维.html

---
## Solution 2:
```Java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int bagWeight = scanner.nextInt();

        int[] weight = new int[n];
        int[] value = new int[n];

        for (int i = 0; i < n; i++) {
            weight[i] = scanner.nextInt();
            value[i] = scanner.nextInt();
        }

        int[] dp = new int[bagWeight + 1];

        for(int j = weight[0]; j <= bagWeight; j++){
            dp[j] = dp[j - weight[0]] + value[0];
        }
        
        for(int i = 1; i < n; i++){
            for(int j = weight[i]; j <= bagWeight; j++){
                dp[j] = Math.max(dp[j], dp[j - weight[i]] + value[i]);
            }
        }

        System.out.println(dp[bagWeight]);
        scanner.close();
    }
}
```
Time complexity: O(mn)  
Space complexity: O(n)
