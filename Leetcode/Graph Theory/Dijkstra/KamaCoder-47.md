## Question:

https://kamacoder.com/problempage.php?pid=1047

---
## Thought 1:
We use dijkstra to do it.

https://programmercarl.com/kamacoder/0047.参会dijkstra朴素.html#思路

---
## Solution 1:
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

---
## Thought 2:
We use a priorityqueue to help us to improve the dijkstra algorithm.

https://programmercarl.com/kamacoder/0047.参会dijkstra堆.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Edge{
    int to;
    int val;
    
    public Edge(int to, int val){
        this.to = to;
        this.val = val;
    }
}

class Pair{
    int first;
    int second;
    
    public Pair(int first, int second){
        this.first = first;
        this.second = second;
    }
}

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        List<List<Edge>> adjList = new ArrayList<>();
        
        for(int i = 0; i <= n; i++){
            adjList.add(new ArrayList());
        }
        
        for(int i = 0; i < m; i++){
            int x = scan.nextInt();
            int y = scan.nextInt();
            int z = scan.nextInt();
            
            adjList.get(x).add(new Edge(y, z));
        }
        
        PriorityQueue<Pair> pq = new PriorityQueue<>(
            (a, b) -> Integer.compare(a.second, b.second)
        );
        
        boolean[] visited = new boolean[n + 1];
        int[] minDist = new int[n + 1];
        Arrays.fill(minDist, Integer.MAX_VALUE);
        minDist[1] = 0;
        
        pq.add(new Pair(1, 0));
        
        while(!pq.isEmpty()){
            Pair curr = pq.poll();
            
            if(visited[curr.first]) continue;
            
            List<Edge> nextNodes = adjList.get(curr.first);
            
            visited[curr.first] = true;
            int second = curr.second;
            
            for(Edge edge : nextNodes){
                int to = edge.to;
                int val = edge.val;
                
                if(!visited[to] && second + val < minDist[to]){
                    minDist[to] = second + val;
                    pq.add(new Pair(to, minDist[to]));
                }
            }
        }
        
        System.out.println(minDist[n] == Integer.MAX_VALUE ? -1 : minDist[n]);
        scan.close();
    }
}
```
Time complexity: O(mlogm)  
Space complexity: O(n + m)
