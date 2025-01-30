## Question:

https://kamacoder.com/problempage.php?pid=1181

---
## Thought:
We use disjoint set union to do it.

https://programmercarl.com/kamacoder/0108.冗余连接.html#思路

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
    }
    
    public boolean isSame(int u, int v){
        u = find(u);
        v = find(v);
        return u == v ? true : false;
    }
}

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        
        Disjoint disjoint = new Disjoint(n + 1);
        
        int resultStart = 0;
        int resultEnd = 0;
        
        for(int i = 0; i <= n; i++){
            int start = scan.nextInt();
            int end = scan.nextInt();
            
            if(!disjoint.isSame(start, end)){
                disjoint.join(start, end);
            }
            else{
                resultStart = start;
                resultEnd = end;
                break;
            }
        }
        
        System.out.println(resultStart + " " + resultEnd);
        
        scan.close();
    }
}
```
Time complexity: O(n)  
Space complexity: O(n)
