## Question:

https://kamacoder.com/problempage.php?pid=1152

---
## Thought 1:
We use bellman-ford to do it.

https://programmercarl.com/kamacoder/0094.城市间货物运输I.html#思路

---
## Solution 1:
```Java
import java.util.*;

class Edge{
    
    int from;
    int to;
    int val;
    
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
        List<Edge> edges = new ArrayList<>();
        
        for(int i = 0; i < m; i++){
            int from = scan.nextInt();
            int to = scan.nextInt();
            int val = scan.nextInt();
            edges.add(new Edge(from, to, val));
        }
        
        int[] minDist = new int[n + 1];
        Arrays.fill(minDist, Integer.MAX_VALUE);
        
        minDist[1] = 0;
        
        for(int i = 0; i < n - 1; i++){
            
            for(Edge edge : edges){
                if(minDist[edge.from] != Integer.MAX_VALUE && minDist[edge.to] > minDist[edge.from] + edge.val){
                    minDist[edge.to] = minDist[edge.from] + edge.val;
                }
            }
        }
        
        System.out.println(minDist[n] == Integer.MAX_VALUE ? "unconnected" : minDist[n]);
        scan.close();
    }
}
```
Time complexity: O(mn)  
Space complexity: O(m + n)

---
## Thought 2:
We use SPFA to do it.

https://programmercarl.com/kamacoder/0094.城市间货物运输I-SPFA.html#背景

---
## Solution 2:
```Java
import java.util.*;


class Main{
    
    static class Edge {
        int to;
        int val;
        public Edge(int to, int val) {
            this.to = to;
            this.val = val;
        }
    }
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        List<List<Edge>> adjList = new ArrayList<>();
        
        for(int i = 0; i <= n; i++){
            adjList.add(new ArrayList<>());
        }
        
        for(int i = 0; i < m; i++){
            int from = scan.nextInt();
            int to = scan.nextInt();
            int val = scan.nextInt();
            adjList.get(from).add(new Edge(to, val));
        }
        
        int[] minDist = new int[n + 1];
        Arrays.fill(minDist, Integer.MAX_VALUE);
        minDist[1] = 0;
        
        Queue<Integer> q = new ArrayDeque<>();
        q.add(1);
        
        boolean[] isInQueue = new boolean[n + 1];
        
        while(!q.isEmpty()){
            int currNode = q.poll();
            
            for(Edge edge : adjList.get(currNode)){
                if(minDist[edge.to] > minDist[currNode] + edge.val){
                    minDist[edge.to] = minDist[currNode] + edge.val;
                    if(!isInQueue[edge.to]){
                        q.add(edge.to);
                        isInQueue[edge.to] = true;
                    }
                }
                
            }
            
            isInQueue[currNode] = false;
        }
        
        System.out.println(minDist[n] == Integer.MAX_VALUE ? "unconnected" : minDist[n]);
        scan.close();
    }
}
```
Time complexity: O(m * k) (k is the average times of each node adding in the pq)  
Space complexity: O(m + n)
