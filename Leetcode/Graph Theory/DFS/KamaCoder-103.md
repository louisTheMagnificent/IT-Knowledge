## Question:

https://kamacoder.com/problempage.php?pid=1175

---
## Thought 1:
We use dfs to do it.

https://programmercarl.com/kamacoder/0103.水流问题.html#思路

---
## Solution 1:
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
        
        boolean[][] pacific = new boolean[n][m];
        boolean[][] atlantic = new boolean[n][m];
        
        for(int i = 0; i < n; i++){
            dfs(graph, pacific, i, 0, Integer.MIN_VALUE);
            dfs(graph, atlantic, i, m - 1, Integer.MIN_VALUE);
        }
        
        for(int j = 0; j < m; j++){
            dfs(graph, pacific, 0, j, Integer.MIN_VALUE);
            dfs(graph, atlantic, n - 1, j, Integer.MIN_VALUE);
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(pacific[i][j] && atlantic[i][j]){
                    System.out.println(i + " " + j);
                }
            }
        }
        
        scan.close();
    }
    
    public static void dfs(int[][] graph, boolean[][] visited, int y, int x, int prevH){
        
        if(x < 0 || x >= graph[0].length || y < 0 || y >= graph.length || visited[y][x]) return;
        if(graph[y][x] < prevH) return;
        
        visited[y][x] = true;
        
        dfs(graph, visited, y + 1, x, graph[y][x]);
        dfs(graph, visited, y - 1, x, graph[y][x]);
        dfs(graph, visited, y, x - 1, graph[y][x]);
        dfs(graph, visited, y, x + 1, graph[y][x]);
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)

---
## Thought 2:
We use bfs to do it.

https://programmercarl.com/kamacoder/0103.水流问题.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Main{
    
    private static class Pair{
        int y; 
        int x;
        
        public Pair(int y, int x){
            this.y = y;
            this.x = x;
        }
    }
    
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
        
        boolean[][] pacific = new boolean[n][m];
        boolean[][] atlantic = new boolean[n][m];
        
        for(int i = 0; i < n; i++){
            bfs(graph, pacific, i, 0);
            bfs(graph, atlantic, i, m - 1);
        }
        
        for(int j = 0; j < m; j++){
            bfs(graph, pacific, 0, j);
            bfs(graph, atlantic, n - 1, j);
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(pacific[i][j] && atlantic[i][j]){
                    System.out.println(i + " " + j);
                }
            }
        }
        
        scan.close();
    }
    
    public static void bfs(int[][] graph, boolean[][] visited, int y, int x){
        
        visited[y][x] = true;
        Queue<Pair> queue = new ArrayDeque<>();
        queue.offer(new Pair(y, x));
        
        while(!queue.isEmpty()){
            
            Pair curr = queue.poll();
            
            int currX = curr.x;
            int currY = curr.y;
            int currH = graph[curr.y][curr.x];
            
            if(currY - 1 >= 0 && !visited[currY - 1][currX] && graph[currY - 1][currX] >= currH){
                visited[currY - 1][currX] = true;
                queue.offer(new Pair(currY - 1, currX));
            }
            
            if(currY + 1 < graph.length && !visited[currY + 1][currX] && graph[currY + 1][currX] >= currH){
                visited[currY + 1][currX] = true;
                queue.offer(new Pair(currY + 1, currX));
            }
            
            if(currX - 1 >= 0 && !visited[currY][currX - 1] && graph[currY][currX - 1] >= currH){
                visited[currY][currX - 1] = true;
                queue.offer(new Pair(currY, currX - 1));
            }
            
            if(currX + 1 < graph[0].length && !visited[currY][currX + 1] && graph[currY][currX + 1] >= currH){
                visited[currY][currX + 1] = true;
                queue.offer(new Pair(currY, currX + 1));
            }
        }
        
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
