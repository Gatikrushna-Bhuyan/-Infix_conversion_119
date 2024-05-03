# -Infix_conversion_119
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String [] args){
        Scanner sc = new Scanner(System.in);
        String exp = sc.nextLine();
        
        //code 
        
        Stack<String> postfix = new Stack<>();
        Stack<String>prefix = new Stack<>();
        Stack<Character> ops = new Stack<>();
        
        for(int i = 0; i< exp.length();i++){
            char ch = exp.charAt(i);
            
            if(ch == '('){
                ops.push(ch);
            }
            else if((ch >= '0' && ch <= '9')|| (ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')){
                postfix.push(ch + ""); 
                
                // characters mn "" (string) add karne se woh string ban jata hn
                
                prefix.push(ch + "");
            }
            else if(ch == ')'){
                // kam tab tab hota rah ta hn jab tak closing bracket na mil jata
                while(ops.peek() != '('){
                    char op = ops.pop();
                    
                    String postv2 = postfix.pop();
                    String postv1 = postfix.pop();
                    String postv = postv1 + postv2 + op;
                    // push in postfix
                    postfix.push(postv);
                    
                    
                    // same in prefix
                    
                    String prev2 = prefix.pop();
                    String prev1 = prefix.pop();
                    String prev = op+ prev1 + prev2;
                    prefix.push(prev);
                    
                }
                ops.pop();
            }
            else if(ch == '+' || ch == '-' || ch == '*' || ch == '/'){
                 while(ops.size() != 0 && ops.peek() != '(' && 
                 precedence(ch) <= precedence(ops.peek())){
                    char op = ops.pop();  //**
                    
                    String postv2 = postfix.pop();
                    String postv1 = postfix.pop();
                    String postv = postv1 + postv2 + op;
                    // push in postfix
                    postfix.push(postv);
                    
                    
                    // same in prefix
                    
                    String prev2 = prefix.pop();
                    String prev1 = prefix.pop();
                    String prev = op+ prev1 + prev2;
                    prefix.push(prev);
                    
                }
                ops.push(ch); //**
                
                
            }
        }
        
        // it might be possible that something has left in th stack , for pocessing 
          while(ops.size() != 0){
                    char op = ops.pop();
                    
                    String postv2 = postfix.pop();
                    String postv1 = postfix.pop();
                    String postv = postv1 + postv2 + op;
                    
                    // push in postfix
                    postfix.push(postv);
                    
                    
                    // same in prefix
                    
                    String prev2 = prefix.pop();
                    String prev1 = prefix.pop();
                    String prev = op+ prev1 + prev2 ;
                    prefix.push(prev);
                    
                }
                System.out.println(postfix.pop());
                System.out.println(prefix.pop());
        
    }
    // function to arrange in precendece 
    public static int precedence(char op){
        if(op == '+' || op == '-'){
          return 1;  
        }
        else if(op == '*' || op == '/'){
           return 2; 
        }
        
        else{
            /* this code will never execute but you have to make it 
            because we are not passing anything other than + - * / 
            */
            /*
            Then why? 
            java will consider what if some other operator will pass , then what will
            return , that's why java might show error , so this 
            'else' is needed 
            */
            // java ki compiler co satisfy karne keliye ye likhna padega 
            
            return 0;
            
        }
    }
}
