## Question:

https://kamacoder.com/problempage.php?pid=1174

---
## Thought 1:
We use bfs to do it.

https://programmercarl.com/kamacoder/0102.沉没孤岛.html#思路

---
## Solution 1:
```Java
import java.util.*;

class Main{
    
    static final int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    
    static class Pair{
        public int x;
        public int y;
        
        public Pair(int x, int y){
            this.x = x;
            this.y = y;
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
        
        
        for(int i = 0; i < n; i++){
            if(graph[i][0] == 1){
                bfs(graph, i, 0);
            }
            
            if(graph[i][m - 1] == 1){
                bfs(graph, i, m - 1);
            }
        }
        
        for(int j = 0; j < m; j++){
            if(graph[0][j] == 1){
                bfs(graph, 0, j);
            }
            
            if(graph[n - 1][j] == 1){
                bfs(graph, n - 1, j);
            }
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1){
                    graph[i][j] = 0;
                }
                else if(graph[i][j] == 2){
                    graph[i][j] = 1;
                }
                if(j != m - 1){
                    System.out.print(graph[i][j] + " ");
                }
                else{
                    System.out.println(graph[i][j]);
                }
            }
        }
        
        scan.close();
    }
    
    public static void bfs(int[][] graph, int y, int x){
        
        graph[y][x] = 2;
        Queue<Pair> queue = new ArrayDeque<>();
        queue.add(new Pair(x, y));

        while(!queue.isEmpty()){
            Pair curr = queue.poll();
            int currX = curr.x;
            int currY = curr.y;
            for(int i = 0; i < 4; i++){
                int nextX = currX + dir[i][0];
                int nextY = currY + dir[i][1];
                if(nextX >= 0 && nextX < graph[0].length && 
                    nextY >= 0 && nextY < graph.length &&
                    graph[nextY][nextX] == 1){
                        graph[nextY][nextX] = 2;
                        queue.add(new Pair(nextX, nextY));
                }
            }
        }
    }
    
}
```
Time complexity: O(mn)  
Space complexity: O(mn)

---
## Thought 2:
We use dfs to do it.

https://programmercarl.com/kamacoder/0102.沉没孤岛.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Main{
    
    static final int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    
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
        
        
        for(int i = 0; i < n; i++){
            if(graph[i][0] == 1){
                dfs(graph, i, 0);
            }
            
            if(graph[i][m - 1] == 1){
                dfs(graph, i, m - 1);
            }
        }
        
        for(int j = 0; j < m; j++){
            if(graph[0][j] == 1){
                dfs(graph, 0, j);
            }
            
            if(graph[n - 1][j] == 1){
                dfs(graph, n - 1, j);
            }
        }
        
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1){
                    graph[i][j] = 0;
                }
                else if(graph[i][j] == 2){
                    graph[i][j] = 1;
                }
                if(j != m - 1){
                    System.out.print(graph[i][j] + " ");
                }
                else{
                    System.out.println(graph[i][j]);
                }
            }
        }
        
        scan.close();
    }
    
    public static void dfs(int[][] graph, int y, int x){
        
        graph[y][x] = 2;
        for(int i = 0; i < 4; i++){
            int nextX = x + dir[i][0];
            int nextY = y + dir[i][1];
            if(nextX >= 0 && nextX < graph[0].length && 
                nextY >= 0 && nextY < graph.length &&
                graph[nextY][nextX] == 1){
                    dfs(graph, nextY, nextX);
                }
        }
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
