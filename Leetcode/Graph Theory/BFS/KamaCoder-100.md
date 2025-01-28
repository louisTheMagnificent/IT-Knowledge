## Question:

https://kamacoder.com/problempage.php?pid=1172

---
## Thought 1:
We use dfs to do it.

https://programmercarl.com/kamacoder/0100.岛屿的最大面积.html#思路

---
## Solution 1:
```Java
import java.util.*;

class Main{
    
    static final int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    static int result = 0;
    static int count = 0;
    
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
        
        boolean[][] check = new boolean[n][m];
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1 && !check[i][j]){
                    check[i][j] = true;
                    dfs(graph, check, i, j);
                    result = Math.max(result, count);
                    count = 0;
                }
            }
        }
        
        System.out.println(result);
        scan.close();
    }
    
    public static void dfs(int[][] graph, boolean[][] check, int y, int x){
        count++;
        
        for(int i = 0; i < 4; i++){
            int nextX = x + dir[i][0];
            int nextY = y + dir[i][1];
            if(nextX >= 0 && nextX < graph[0].length && 
                nextY >= 0 && nextY < graph.length &&
                graph[nextY][nextX] == 1 && !check[nextY][nextX]){
                    check[nextY][nextX] = true;
                    dfs(graph, check, nextY, nextX);
                }
        }
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)

---
## Thought 2:
We use bfs to do it.

https://programmercarl.com/kamacoder/0100.岛屿的最大面积.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Main{
    
    static final int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    static int result = 0;
    static int count = 0;
    
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
        
        boolean[][] check = new boolean[n][m];
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1 && !check[i][j]){
                    check[i][j] = true;
                    bfs(graph, check, i, j);
                    result = Math.max(result, count);
                    count = 0;
                }
            }
        }
        
        System.out.println(result);
        scan.close();
    }
    
    public static void bfs(int[][] graph, boolean[][] check, int y, int x){
        count++;
        
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
                    graph[nextY][nextX] == 1 && !check[nextY][nextX]){
                        count++;
                        check[nextY][nextX] = true;
                        queue.add(new Pair(nextX, nextY));
                }
            }
        }
    }
    
    
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
