## Question: 

https://kamacoder.com/problempage.php?pid=1064

---
## Thought: 

https://programmercarl.com/kamacoder/0054.替换数字.html#其他语言版本

---
## Solution:
```Java
import java.util.Scanner;

public class Main{
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.next();
        System.out.println(replaceNumber(s));
        scanner.close();
    }
    
    public static String replaceNumber(String s){
        StringBuilder sb = new StringBuilder();
        int curr = 0;
        while(curr < s.length()){
            char c = s.charAt(curr);
            if(c >= 48 && c <=57){
                sb.append("number");
            }
            else{
                sb.append(c);
            }
            curr++;
        }
        return sb.toString();
    }
    
}
```
Time complexity: O(n)  
Space complexity: O(n)
