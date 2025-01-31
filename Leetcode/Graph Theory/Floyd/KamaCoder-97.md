## Question:

https://kamacoder.com/problempage.php?pid=1155

---
## Thought 1:
We use floyd to do it.

https://programmercarl.com/kamacoder/0097.小明逛公园.html#思路

---
## Solution 1:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan =  new Scanner(System.in);
        
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        int[][][] grid = new int[n + 1][n + 1][n + 1];
        
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= n; j++){
                for(int k = 0; k <= n; k++){
                    grid[i][j][k] = 1000000;
                }
            }
        }
        
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            int val = scan.nextInt();
            grid[start][end][0] = val;
            grid[end][start][0] = val;
        }
        
        for(int k = 1; k <= n; k++){
            for(int i = 1; i <= n; i++){
                for(int j = 1; j <= n; j++){
                    grid[i][j][k] = Math.min(grid[i][j][k - 1], grid[i][k][k - 1] + grid[k][j][k - 1]);
                }
            }
        }
        
        int num = scan.nextInt();
        for(int i = 0; i < num; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            if(grid[start][end][n] == 1000000) System.out.println("-1");
            else System.out.println(grid[start][end][n]);
        }
        
        scan.close();
    }
}
```
Time complexity: O(n<sup>3</sup>)  
Space complexity: O(n<sup>3</sup>)

---
## Thought 2:
We use floyd to do it but fewer dimention array.

https://programmercarl.com/kamacoder/0097.小明逛公园.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan =  new Scanner(System.in);
        
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        int[][] grid = new int[n + 1][n + 1];
        
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= n; j++){
                grid[i][j] = 1000000;
            }
        }
        
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            int val = scan.nextInt();
            grid[start][end] = val;
            grid[end][start] = val;
        }
        
        for(int k = 1; k <= n; k++){
            for(int i = 1; i <= n; i++){
                for(int j = 1; j <= n; j++){
                    grid[i][j] = Math.min(grid[i][j], grid[i][k] + grid[k][j]);
                }
            }
        }
        
        int num = scan.nextInt();
        for(int i = 0; i < num; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            if(grid[start][end] == 1000000) System.out.println("-1");
            else System.out.println(grid[start][end]);
        }
        
        scan.close();
    }
}
```
Time complexity: O(n<sup>3</sup>)  
Space complexity: O(n<sup>2</sup>)
