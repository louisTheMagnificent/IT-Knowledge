## Question:

https://kamacoder.com/problempage.php?pid=1182

---
## Thought: 
We use adjList and Disjoint set union to do it.

https://programmercarl.com/kamacoder/0109.冗余连接II.html#思路

---
## Solution:
```Java
import java.util.*;

class Disjoint{
    
    private int[] father;
    
    public Disjoint(int n){
        this.father = new int[n];
        for(int i = 0; i < n; i++){
            father[i] = i;
        }
    }
    
    public int find(int i){
        return i == father[i] ? i : (father[i] = find(father[i]));
    }
    
    public void join(int u, int v){
        u = find(u);
        v = find(v);
        if(u == v) return;
        father[v] = u;
        return;
    }
    
    public boolean isSame(int u, int v){
        u = find(u);
        v = find(v);
        return u == v ? true : false;
    }
}

class Edge{
    
    int start;
    int end;
    
    public Edge(int start, int end){
        this.start = start;
        this.end = end;
    }
}

class Main{
    
    public static void main(String[] args){
        
        Scanner scan = new Scanner(System.in);
        
        int n = scan.nextInt();
        
        int[] inDegree = new int[n + 1];
        List<Edge> edges = new ArrayList<>();
        int inDegreeTwo = 0;
        Edge potentialRemove = new Edge(0, 0);
        
        for(int i = 0; i < n; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            if(inDegree[end] == 1){
                inDegreeTwo = end;
                potentialRemove.start = start;
                potentialRemove.end = end;
            }
            inDegree[end]++;
            edges.add(new Edge(start, end));
            
        }
        
        Edge result = null;
        if(inDegreeTwo == 0){
            result = getRemoveEdge(edges);
        }
        else{
            result = isTreeAfterRemove(edges, potentialRemove);
        }
        
        System.out.println(result.start + " " + result.end);
        scan.close();
    }
    
    public static Edge isTreeAfterRemove(List<Edge> edges, Edge potentialRemove){
        
        int n = edges.size();
        Edge another = new Edge(0, 0);
        another.end = potentialRemove.end;
        
        Disjoint disjoint = new Disjoint(n + 1);
        for(Edge edge : edges){
            if(edge.end == potentialRemove.end){
                if(edge.start == potentialRemove.start){
                    continue;
                }
                else{
                    another.start = edge.start;
                }
            }
            disjoint.join(edge.start, edge.end);
        }
        
        if(disjoint.isSame(potentialRemove.start, potentialRemove.end)) return potentialRemove;
        else return another;
    }
    
    public static Edge getRemoveEdge(List<Edge> edges){
        Disjoint disjoint = new Disjoint(edges.size() + 1);
        for(Edge edge : edges){
            int start = edge.start;
            int end = edge.end;
            if(disjoint.isSame(start, end)){
                return edge;
            }
            else{
                disjoint.join(start, end);
            }
        }
        return null;
    }
}
```
Time complexity: O(n)  
Space complexity: O(n)
