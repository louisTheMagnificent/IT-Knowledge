## Question: 

https://kamacoder.com/problempage.php?pid=1170

---
## Thought:

https://programmercarl.com/kamacoder/0098.所有可达路径.html

---
## Solution:
```Java
import java.util.*;

public class Main{
    
    private static List<List<Integer>> result;
    private static List<Integer> curr;
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        
        List<List<Integer>> graph = new ArrayList<>(n + 1);
        
        result = new ArrayList<>();
        curr = new ArrayList<>();
        
        for(int i = 0; i <= n; i++){
            graph.add(new ArrayList<>());
        }
        
        for(int i = 0; i < m; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            graph.get(start).add(end);
        }
        
        curr.add(1);
        
        dfs(graph, 1, n);
        
        if(result.size() == 0){
            System.out.println("-1");
        }
        
        for(int i = 0; i < result.size(); i++){
            List<Integer> currResult = result.get(i);
            for(int j = 0; j < currResult.size() - 1; j++){
                System.out.print(currResult.get(j) + " ");
            }
            System.out.println(currResult.get(currResult.size() - 1));
        }
        
        scan.close();
    }
    
    public static void dfs(List<List<Integer>> graph, int start, int end){
        if(start == end){
            result.add(new ArrayList<>(curr));
            return;
        }
        
        List<Integer> currNode = graph.get(start);
        
        for(int i = 0; i < currNode.size(); i++){
            int next = currNode.get(i);
            boolean isShown = false;
            for(int j = 0; j < curr.size(); j++){
                if(curr.get(j) == next){
                    isShown = true;
                    break;
                }
            }
            if(isShown) continue;
            
            curr.add(next);
            dfs(graph, next, end);
            curr.remove(curr.size() - 1);

        }
        
        return;
    }
}
```
Time complexity: O(mn)  
Space complexity: O(m + n)
