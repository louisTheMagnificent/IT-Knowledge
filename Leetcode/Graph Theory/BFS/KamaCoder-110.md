## Question:

https://kamacoder.com/problempage.php?pid=1183

---
## Thought:
We use bfs to do it.

https://programmercarl.com/kamacoder/0110.字符串接龙.html#思路

---
## Solution:
```Java
import java.util.*;

class Main{
    
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        scan.nextLine();
        String start = scan.next();
        String end = scan.next();
        scan.nextLine();
        Set<String> set = new HashSet<>();
        set.add(start);
        set.add(end);
        for(int i = 0; i < n; i++){
            set.add(scan.nextLine());
        }
        
        int result = bfs(set, start, end);
        
        System.out.println(result);
        
    }
    
    private static int bfs(Set<String> wordList, String start, String end){
        int length = 1;
        Set<String> set = new HashSet<>(wordList);
        Set<String> visited = new HashSet<>();
        Queue<String> queue = new LinkedList<>();
        visited.add(start);
        queue.add(start);
        queue.add(null);
        while(!queue.isEmpty()){
            String node = queue.poll();
            if (node == null) {
                if (!queue.isEmpty()) {
                    length++;
                    queue.add(null);
                }
                continue;
            }
            
            char[] charArray = node.toCharArray();
            
            for (int i = 0; i < charArray.length; i++) {
                char old = charArray[i];
                for (char j = 'a'; j <= 'z'; j++) {
                    charArray[i] = j;
                    String newWord = new String(charArray);
                    if (set.contains(newWord) && !visited.contains(newWord)) {
                        queue.add(newWord);
                        visited.add(newWord);
                        if (newWord.equals(end)) return length + 1;
                    }
                }
                charArray[i] = old;
            }
        }
        
        return 0;
    }
}
```
Time complexity: O(mn)  
Space complexity: O(mn)
