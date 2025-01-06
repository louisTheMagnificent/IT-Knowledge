## Question:

https://kamacoder.com/problempage.php?pid=1065

---
## Thought:

https://programmercarl.com/kamacoder/0055.右旋字符串.html#拓展

---
## Solution:
```Java
import java.util.Scanner;

public class Main{
    
    public static void main (String[] args) {
        
        Scanner in = new Scanner(System.in);
        int n = Integer.parseInt(in.nextLine());
        String s = in.nextLine();
        
        int length = s.length();
        
        n = n % length;
        if(n == 0){
            System.out.println(s);
            in.close();
            return;
        }
        
        StringBuilder sb = new StringBuilder();
        
        int start = length - n;
        while(start < length){
            sb.append(s.charAt(start));
            start++;
        }
        
        start = 0;
        while(start < length - n){
            sb.append(s.charAt(start));
            start++;            
        }
        
        System.out.println(sb.toString());
        in.close();
    }
    
}
```
Time complexity: O(n)  
Space complexity: O(n)
