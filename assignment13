import java.util.Stack;
import java.util.Queue;
import java.util.LinkedList;
import java.util.HashMap;
import java.util.Map;

public class ShuntingYard {

    private static final Map<Character, Integer> PRECEDENCE = new HashMap<>();
    static {
        PRECEDENCE.put('+', 1);
        PRECEDENCE.put('-', 1);
        PRECEDENCE.put('*', 2);
        PRECEDENCE.put('/', 2);
        PRECEDENCE.put('^', 3);
    }

    public static Queue<Character> convertToPostfix(String infix) {
        Queue<Character> postfix = new LinkedList<>();
        Stack<Character> operators = new Stack<>();

        for (char token : infix.toCharArray()) {
            if (Character.isDigit(token)) {
                postfix.add(token);
            } else if (token == '(') {
                operators.push(token);
            } else if (token == ')') {
                while (!operators.isEmpty() && operators.peek() != '(') {
                    postfix.add(operators.pop());
                }
                operators.pop(); // Pop the '('
            } else if (PRECEDENCE.containsKey(token)) {
                while (!operators.isEmpty() && isHigherPrecedence(operators.peek(), token)) {
                    postfix.add(operators.pop());
                }
                operators.push(token);
            }
        }

        while (!operators.isEmpty()) {
            postfix.add(operators.pop());
        }

        return postfix;
    }

    private static boolean isHigherPrecedence(char op1, char op2) {
        if (!PRECEDENCE.containsKey(op1)) {
            return false;
        }
        return PRECEDENCE.get(op1) >= PRECEDENCE.get(op2);
    }

    public static void main(String[] args) {
        String infixExpression = "3+4*2/(1-5)^2";
        System.out.println("Infix: " + infixExpression);

        Queue<Character> postfix = convertToPostfix(infixExpression);
        System.out.print("Postfix: ");
        while (!postfix.isEmpty()) {
            System.out.print(postfix.poll());
        }
    }
}
