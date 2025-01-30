## Question:

https://kamacoder.com/problempage.php?pid=1047

---
## Thought:
We use dijkstra to do it.

https://programmercarl.com/kamacoder/0047.参会dijkstra朴素.html#思路

---
## Solution:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        int[][] graph = new int[n + 1][n + 1];
        for(int i = 0; i <= n; i++){
            Arrays.fill(graph[i], Integer.MAX_VALUE);
        }
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            int value = scan.nextInt();
            graph[start][end] = value;
        }
        
        int[] minDist = new int[n + 1];
        Arrays.fill(minDist, Integer.MAX_VALUE);
        minDist[1] = 0;
        boolean[] visited = new boolean[n + 1];
        
        for(int i = 1; i <= n; i++){
            int minVal = Integer.MAX_VALUE;
            int curr = 1;
            
            for(int j = 1; j <= n; j++){
                if(!visited[j] && minDist[j] < minVal){
                    curr = j;
                    minVal = minDist[j];
                }
            }
            
            if(curr == 1 && visited[curr]) break;
            
            visited[curr] = true;
            
            for(int j = 1; j <= n; j++){
                if(!visited[j] && graph[curr][j] != Integer.MAX_VALUE && minDist[curr] + graph[curr][j] < minDist[j]){
                    minDist[j] = minDist[curr] + graph[curr][j];
                }
            }
        }
        
        System.out.println(minDist[n] == Integer.MAX_VALUE ? "-1" : minDist[n]);
        scan.close();
    }
}
```
Time complexity: O(n<sup>2</sup>)  
Space complexity: O(n<sup>2</sup>)
