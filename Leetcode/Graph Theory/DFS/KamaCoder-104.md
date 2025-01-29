## Question:

https://kamacoder.com/problempage.php?pid=1176

---
## Thought 1:
We use dfs to do it.

https://programmercarl.com/kamacoder/0104.建造最大岛屿.html#思路

---
## Solution 1:
```Java
import java.util.*;

class Main{
    
    private static int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private static int count = 0;
    
    public static void dfs(int[][] graph, int y, int x, int num){
        
        graph[y][x] = num;
        count++;
        
        for(int i = 0; i < 4; i++){
            int nextX = x + dir[i][0];
            int nextY = y + dir[i][1];
            if(nextX >= graph[0].length || nextX < 0 || 
                nextY >= graph.length || nextY < 0 ||
                graph[nextY][nextX] != 1){
                    continue;
                }
            dfs(graph, nextY, nextX, num);
        }
        
        return;
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
        
        int mark = 2;
        Map<Integer, Integer> size = new HashMap<>(); 
        int result = 0;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1){
                    dfs(graph, i, j, mark);
                    size.put(mark, count);
                    result = Math.max(result, count);
                    mark++;
                    count = 0;
                }
            }
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 0){
                    Set<Integer> connected = new HashSet<>();
                    for(int k = 0; k < 4; k++){
                        int nextX = j + dir[k][0];
                        int nextY = i + dir[k][1];
                        if(nextX >= graph[0].length || nextX < 0 || 
                            nextY >= graph.length || nextY < 0 ||
                            graph[nextY][nextX] == 0){
                                continue;
                            }
                        int currIsland = graph[nextY][nextX];
                        connected.add(currIsland);
                    }
                    int currSize = 1;
                    for(int curr : connected){
                        currSize += size.get(curr);
                    }
                    result = Math.max(result, currSize);
                }
            }
        }
        
        System.out.println(result);
    }
    
}
```
Time complexity: O(mn)  
Space complexity: O(mn)

---
## Thought 2:
We use bfs to do it.

https://programmercarl.com/kamacoder/0104.建造最大岛屿.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Main{
    
    private static int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private static int count = 0;
    
    private static class Pair{
        int x;
        int y;
        
        public Pair(int y, int x){
            this.y = y;
            this.x = x;
        }
    }
    
    public static void bfs(int[][] graph, int y, int x, int num){
        
        Queue<Pair> queue = new LinkedList<>();
        queue.offer(new Pair(y, x));
        graph[y][x] = num;
        
        while(!queue.isEmpty()){
            Pair curr = queue.poll();
            int currX = curr.x;
            int currY = curr.y;
            count++;
            for(int i = 0; i < 4; i++){
                int nextX = currX + dir[i][0];
                int nextY = currY + dir[i][1];
                if(nextX >= graph[0].length || nextX < 0 || 
                    nextY >= graph.length || nextY < 0 ||
                    graph[nextY][nextX] != 1){
                        continue;
                    }
                graph[nextY][nextX] = num;
                queue.offer(new Pair(nextY, nextX));
            }
            
        }
        
        return;
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
        
        int mark = 2;
        Map<Integer, Integer> size = new HashMap<>(); 
        int result = 0;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 1){
                    bfs(graph, i, j, mark);
                    size.put(mark, count);
                    result = Math.max(result, count);
                    mark++;
                    count = 0;
                }
            }
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(graph[i][j] == 0){
                    Set<Integer> connected = new HashSet<>();
                    for(int k = 0; k < 4; k++){
                        int nextX = j + dir[k][0];
                        int nextY = i + dir[k][1];
                        if(nextX >= graph[0].length || nextX < 0 || 
                            nextY >= graph.length || nextY < 0 ||
                            graph[nextY][nextX] == 0){
                                continue;
                            }
                        int currIsland = graph[nextY][nextX];
                        connected.add(currIsland);
                    }
                    int currSize = 1;
                    for(int curr : connected){
                        currSize += size.get(curr);
                    }
                    result = Math.max(result, currSize);
                }
            }
        }
        
        System.out.println(result);
        scan.close();
    }
    
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
