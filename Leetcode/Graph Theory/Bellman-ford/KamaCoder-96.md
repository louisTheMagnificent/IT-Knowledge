## Question:

https://kamacoder.com/problempage.php?pid=1154

---
## Thought 1:
We use bellman-ford to do it.

https://programmercarl.com/kamacoder/0096.城市间货物运输III.html#思路

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
        
        List<Edge> edges = new ArrayList<>();
        
        for(int i = 0; i < m; i++){
            int from = scan.nextInt();
            int to = scan.nextInt();
            int val = scan.nextInt();
            edges.add(new Edge(from, to, val));
        }
        
        int start = scan.nextInt();
        int end = scan.nextInt();
        int k = scan.nextInt();
        
        int[] minDist = new int[n + 1];
        int[] prevMinDist = new int[n + 1];
        
        Arrays.fill(minDist, Integer.MAX_VALUE);
        
        minDist[start] = 0;
        boolean updated = false;
        
        for(int i = 0; i < k + 1; i++){
            updated = false;
            prevMinDist = Arrays.copyOf(minDist, n + 1);
            for(Edge edge : edges){
                if(prevMinDist[edge.from] != Integer.MAX_VALUE && minDist[edge.to] > prevMinDist[edge.from] + edge.val){
                    minDist[edge.to] = prevMinDist[edge.from] + edge.val;
                    updated = true;
                }
            }
            if(!updated) break;
        }
        
        System.out.println(minDist[end] == Integer.MAX_VALUE ? "unreachable" : minDist[end]);
        scan.close();
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)

---
## Thought 2:
We use SPFA to do it.

https://programmercarl.com/kamacoder/0096.城市间货物运输III.html#思路v

---
## Solution 2:
```Java
