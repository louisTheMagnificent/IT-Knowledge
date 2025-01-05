## Question: 

https://kamacoder.com/problempage.php?pid=1070

---
## Thought:

https://programmercarl.com/kamacoder/0058.区间和.html#其他语言版本

---
## Solution:
```Java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] array = new int[n];
        int[] sum = new int[n];

        int presum = 0;
        for (int i = 0; i < n; i++) {
            array[i] = scanner.nextInt();
            presum += array[i];
            sum[i] = presum;
        }

        while(scanner.hasNextInt()){
            int a = scanner.nextInt();
            int b = scanner.nextInt();
            int currSum;
            if(a == 0){
                currSum = sum[b];
            }
            else{
                currSum = sum[b] - sum[a - 1];
            }
            
            System.out.println(currSum);
        }

        scanner.close();
    }
}
```
Time complexity: O(n + m)  
Space complexity: O(n)
