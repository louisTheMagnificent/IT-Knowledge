## Question: 

https://kamacoder.com/problempage.php?pid=1177

---
## Thought:
We use bfs to do it.

https://programmercarl.com/kamacoder/0105.有向图的完全可达性.html#思路

---
## Solution:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int k = scan.nextInt();
        
        List<List<Integer>> adjList = new ArrayList<>();
        Set<Integer> visited = new HashSet<>();
        
        for(int i = 0; i <= n; i++){
            adjList.add(new ArrayList<>());
        }
        
        for(int i = 0; i < k; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            adjList.get(start).add(end);
        }
        
        Queue<Integer> queue = new ArrayDeque<>();
        
        queue.add(1);
        visited.add(1);
        int num = 1;
        
        while(!queue.isEmpty()){
            int curr = queue.poll();
            List<Integer> nextNodes = adjList.get(curr);
            
            for(int i = 0; i < nextNodes.size(); i++){
                int next = nextNodes.get(i);
                if(!visited.contains(next)){
                    queue.add(next);
                    visited.add(next);
                    num++;
                }
            }
            
            if(num == n) break;
        }
        
        System.out.println(num == n ? "1" : "-1");
        
        scan.close();
    }
    
}
```
Time complexity: O(n + k)  
Space complexity: O(n + k)
