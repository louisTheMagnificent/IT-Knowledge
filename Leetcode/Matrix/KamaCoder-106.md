## Question: 

https://kamacoder.com/problempage.php?pid=1178

---
## Thought:

https://programmercarl.com/kamacoder/0106.岛屿的周长.html#思路

---
## Solution:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        int[][] graph = new int[n][m];
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                graph[i][j] = scan.nextInt();
            }
        }
        
        int perimeter = 0;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1){
                    if(i - 1 < 0 || graph[i - 1][j] == 0){
                        perimeter++;
                    }
                    if(i + 1 == n || graph[i + 1][j] == 0){
                        perimeter++;
                    }
                    if(j - 1 < 0 || graph[i][j - 1] == 0){
                        perimeter++;
                    }
                    if(j + 1 == m || graph[i][j + 1] == 0){
                        perimeter++;
                    }
                }
            }
        }
        System.out.println(perimeter);
        
        scan.close();
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
