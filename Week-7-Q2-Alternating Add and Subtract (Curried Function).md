#  Problem  - Alternating Add and Subtract (Curried Function) 
#  **In This Question I take help from GPT** 
##  Statement  -
You are asked to implement a function add_subtract that works in a curried style and
alternately adds and subtracts the numbers passed to it.
• The first number is always added (considered as the starting point).
• The second number is subtracted.
• The third number is added.
• The fourth number is subtracted.
• And so on, alternating between addition and subtraction.
##  Examples
add_subtract(7)
Output: 7
add_subtract(1)(2)(3)
Steps: 1 + 2 - 3 = 0
Output: 0
add_subtract(-5)(10)(3)(9)
Steps: -5 + 10 - 3 + 9 = 11
Output: 11
##  Code 
```
public class AlternatingSum {
    private int sum;
    private boolean addNext; // true -> add, false -> subtract

    // Private constructor so we control initialization
    private AlternatingSum(int firstNum) {
        this.sum = firstNum;
        this.addNext = false; // next operation should be subtraction
    }

    // Static method to start the chain
    public static AlternatingSum add_subtract(int num) {
        return new AlternatingSum(num);
    }

    // Chained call method
    public AlternatingSum add_subtract(int num) {
        if (addNext) {
            sum += num;
        } else {
            sum -= num;
        }
        addNext = !addNext; // flip for next call
        return this;
    }

    // Return result when printed
    @Override
    public String toString() {
        return String.valueOf(sum);
    }

    public static void main(String[] args) {
        System.out.println(add_subtract(7));                 // 7
        System.out.println(add_subtract(1).add_subtract(2).add_subtract(3));  // 0
        System.out.println(add_subtract(-5).add_subtract(10).add_subtract(3).add_subtract(9)); // 11
        System.out.println(add_subtract(5).add_subtract(6).add_subtract(7)); // 4
    }
}

```
