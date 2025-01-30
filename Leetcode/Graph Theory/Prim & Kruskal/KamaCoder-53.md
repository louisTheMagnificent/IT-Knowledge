## Question:

https://kamacoder.com/problempage.php?pid=1053

---
## Thought 1:
We use Prim to do it.

https://programmercarl.com/kamacoder/0053.寻宝-prim.html#解题思路

---
## Solution 1:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int v = scan.nextInt();
        int e = scan.nextInt();
        
        int[] minDist = new int[v + 1];
        int[][] graph = new int[v + 1][v + 1];
        for(int i = 0; i <= v; i++){
            Arrays.fill(graph[i], 10001);
        }
        Arrays.fill(minDist, 10001);
        boolean[] isInTree = new boolean[v + 1];
        
        for(int i = 0; i < e; i++){
            int x = scan.nextInt();
            int y = scan.nextInt();
            int k = scan.nextInt();
            graph[x][y] = k;
            graph[y][x] = k;
        }
        
        for(int i = 1; i < v; i++){
            int curr = -1;
            int minVal = Integer.MAX_VALUE;
            
            for(int j = 1; j <= v; j++){
                if(!isInTree[j] && minDist[j] < minVal){
                    curr = j;
                    minVal = minDist[j];
                }
            }
            
            isInTree[curr] = true;
            
            for(int j = 1; j <= v; j++){
                if(!isInTree[j]){
                    minDist[j] = Math.min(minDist[j], graph[curr][j]);
                }
            }
        }
        
        int result = 0;
        for(int i = 2; i <= v; i++){
            result += minDist[i];
        }
        
        System.out.println(result);
        scan.close();
    }
}
```
Time complexity: O(n<sup>2</sup>)  
Space complexity: O(n<sup>2</sup>)

---
## Thought 2:
We use Kruskal to do it.

https://programmercarl.com/kamacoder/0053.寻宝-Kruskal.html#解题思路

---
## Solution 2:
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
    int left;
    int right;
    int distance;
    
    public Edge(int left, int right, int distance){
        this.left = left;
        this.right = right;
        this.distance = distance;
    }
}

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int v = scan.nextInt();
        int e = scan.nextInt();
        
        List<Edge> edges = new ArrayList<>();
        Disjoint disjoint = new Disjoint(v + 1);

        for(int i = 0; i < e; i++){
            int x = scan.nextInt();
            int y = scan.nextInt();
            int k = scan.nextInt();
            
            edges.add(new Edge(x, y, k));
        }
        
        int result = 0;
        
        edges.sort(Comparator.comparingInt(edge -> edge.distance));
        
        for(int i = 0; i < e; i++){
            Edge curr = edges.get(i);
            int left = curr.left;
            int right = curr.right;
            if(!disjoint.isSame(left, right)){
                result += curr.distance;
                disjoint.join(left, right);
            }
            else continue;
        }
        
        System.out.println(result);
        scan.close();
    }
}
```
Time complexity: O(nlogn)  
Space complexity: O(m + n)
