## Question: 

https://kamacoder.com/problempage.php?pid=1203

---
## Thought:
We use A* to do it.

https://programmercarl.com/kamacoder/0126.骑士的攻击astar.html#思路

---
## Solution:
```Java
import java.util.*;

class Knight{
    
    int x, y;
    int g, h, f;
    
    public Knight(int x, int y, int g, int h){
        this.x = x;
        this.y = y;
        this.g = g;
        this.h = h;
        this.f = g + h;
    }
}

class Main{
    
    private static PriorityQueue<Knight> pq;
    private static int[][] dir = {{-2, -1}, {-1, -2}, {1, 2}, {2, 1}, 
                                    {-2, 1}, {1, -2}, {-1, 2}, {2, -1}};
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int m = scan.nextInt();
        
        int[][] grid = new int[1001][1001];
        
        while(m-- > 0){
            int startY = scan.nextInt();
            int startX = scan.nextInt();
            int endY = scan.nextInt();
            int endX = scan.nextInt();
            aStar(startY, startX, endY, endX);
        }
        
        scan.close();
    }
    
    public static int Heuristic(int startY, int startX, int endY, int endX){
        return (startY - endY) * (startY - endY) + (startX - endX) * (startX - endX);
    }
    
    public static void aStar(int startY, int startX, int endY, int endX){
        
        Knight k = new Knight(startX, startY, 0, Heuristic(startY, startX, endY, endX));
        pq = new PriorityQueue<>(
            (a, b) -> Integer.compare(a.f, b.f)
        );
        
        pq.add(k);
        int[][] board = new int[1001][1001];
        
        while(!pq.isEmpty()){
            Knight curr = pq.poll();
            
            if(curr.x == endX && curr.y == endY) break;
            
            for(int i = 0; i < 8; i++){
                int nextY = curr.y + dir[i][0];
                int nextX = curr.x + dir[i][1];
                if(nextY < 1 || nextY >= 1001 || nextX < 1 || nextX >= 1001) continue;
                
                if(board[nextY][nextX] == 0){
                    board[nextY][nextX] = board[curr.y][curr.x] + 1;
                    Knight next = new Knight(nextX, nextY, curr.g + 5, Heuristic(nextY, nextX, endY, endX));
                    pq.add(next);
                }
            }
        }
        
        System.out.println(board[endY][endX]);
        return;
    }
}
```
Time complexity: O(nlogn)  
Space complexity: O(result)
