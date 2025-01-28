## Question:

https://kamacoder.com/problempage.php?pid=1191

---
## Thought: 
We use topological sort to do it.

https://programmercarl.com/kamacoder/0117.软件构建.html#拓扑排序的背景

---
## Solution:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        List<List<Integer>> adjList = new ArrayList<>();
        List<Integer> result = new ArrayList<>();
        
        for(int i = 0; i < n; i++){
            adjList.add(new ArrayList<>());
        }
        
        int[] inDegree = new int[n];
        
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            adjList.get(start).add(end);
            inDegree[end]++;
        }
        
        Queue<Integer> queue = new ArrayDeque<>();
        
        for(int i = 0; i < n; i++){
            if(inDegree[i] == 0) queue.offer(i);
        }
        
        while(!queue.isEmpty()){
            int curr = queue.poll();
            result.add(curr);
            List<Integer> list = adjList.get(curr);
            for(int i = 0; i < list.size(); i++){
                int next = list.get(i);
                inDegree[next]--;
                if(inDegree[next] == 0) queue.offer(next);
            }
        }
        
        if(result.size() != n){
            System.out.println("-1");
        }
        
        else{
            for(int i = 0; i < result.size() - 1; i++){
                System.out.print(result.get(i) + " ");
            }
            System.out.print(result.get(result.size() - 1));
        }
        
        scan.close();
    }
}
```
Time compleixty: O(m + n)  
Space complexity: O(m + n)  
