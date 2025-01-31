## Question:

https://kamacoder.com/problempage.php?pid=1153

---
## Thought 1: 
We use bellman-ford to do it.

https://programmercarl.com/kamacoder/0095.城市间货物运输II.html#思路

---
## Solution 1:
```Java
import java.util.*;

class Edge{
    
    public final int from;
    public final int to;
    public final int val;
    
    public Edge(int from, int to, int val){
        this.from = from;
        this.to = to;
        this.val = val;
    }
}

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        List<Edge> graph = new ArrayList<>();
        
        
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            int value = scan.nextInt();
            graph.add(new Edge(start, end, value));
        }
        
        int[] minDist = new int[n + 1];
        Arrays.fill(minDist, Integer.MAX_VALUE);
        minDist[1] = 0;
        boolean flag = false;
        boolean updated;
        
        for(int i = 0; i < n; i++){
            
            updated = false;
            for(Edge edge : graph){
                if(i < n - 1){
                    if(minDist[edge.from] != Integer.MAX_VALUE && minDist[edge.to] > minDist[edge.from] + edge.val){
                        minDist[edge.to] = minDist[edge.from] + edge.val;
                        updated = true;
                    }
                }
                else{
                    if(minDist[edge.from] != Integer.MAX_VALUE && minDist[edge.to] > minDist[edge.from] + edge.val){
                        flag = true;
                        break;
                    }
                }
            }
            if(!updated) break;
        }
        
        if(flag) System.out.println("circle");
        else System.out.println(minDist[n] == Integer.MAX_VALUE ? "unconnected" : minDist[n]);
        
        scan.close();
    }
}
```
Time complexity: O(mn)  
Space complexity: O(n + m)

---
## Thought 2:
We use SPFA to do it.

https://programmercarl.com/kamacoder/0095.城市间货物运输II.html#思路

---
## Solution 2:
```Java
import java.util.*;

class Edge{
    
    public final int to;
    public final int val;
    
    public Edge(int to, int val){
        this.to = to;
        this.val = val;
    }
}

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        List<List<Edge>> adjList = new ArrayList<>();
        
        for(int i = 0; i <= n; i++){
            adjList.add(new ArrayList<>());
        }
        
        
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            int value = scan.nextInt();
            adjList.get(start).add(new Edge(end, value));
        }
        
        int[] minDist = new int[n + 1];
        Arrays.fill(minDist, Integer.MAX_VALUE);
        minDist[1] = 0;
        
        Queue<Integer> queue = new ArrayDeque<>();
        queue.offer(1);
        
        boolean[] isInQueue = new boolean[n + 1];
        
        int[] count = new int[n + 1];
        count[1]++;
        boolean flag = false;
        isInQueue[1] = true;
        
        while(!queue.isEmpty()){
            int curr = queue.poll();
            isInQueue[curr] = false;
            for(Edge edge : adjList.get(curr)){
                if(minDist[edge.to] > minDist[curr] + edge.val){
                    minDist[edge.to] = minDist[curr] + edge.val;
                    
                    if(!isInQueue[edge.to]){
                        queue.offer(edge.to);
                        count[edge.to]++;
                        isInQueue[edge.to] = true;
                        
                    }
                    if(count[edge.to] == n){
                        flag = true;
                        while(!queue.isEmpty()) queue.poll();
                        break;
                    }
                }
            }
        }
        
        if(flag) System.out.println("circle");
        else System.out.println(minDist[n] == Integer.MAX_VALUE ? "unconnected" : minDist[n]);
        
        scan.close();
    }
}
```
Time complexity: O(n<sup>2</sup>)  
Space complexity: O(m + n)
