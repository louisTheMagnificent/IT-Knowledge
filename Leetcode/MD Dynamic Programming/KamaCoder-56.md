## Question:

https://kamacoder.com/problempage.php?pid=1066

---
## Thought:
We use md dp to do it but only 1d array.

https://programmercarl.com/背包问题理论基础多重背包.html

---
## Solution:
```Java
import java.util.Scanner;
class Main{
    public static void main(String [] args) {
        Scanner sc = new Scanner(System.in);

        int bagWeight, n;
        
        bagWeight = sc.nextInt();
        n = sc.nextInt();
        int[] weight = new int[n];
        int[] value = new int[n];
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) weight[i] = sc.nextInt();
        for (int i = 0; i < n; i++) value[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();

        int[] dp = new int[bagWeight + 1];
        
        for(int i = 0; i < n; i++){
            for(int j = bagWeight; j >= weight[i]; j--){
                for(int k = 1; k <= nums[i] && j >= k * weight[i]; k++){
                    dp[j] = Math.max(dp[j], dp[j - k * weight[i]] + k * value[i]);   
                }
            }
        }
        
        System.out.println(dp[bagWeight]);
        
        sc.close();

    }
}
```
Time complexity: O(mnk)   
Space complexity: O(n)
