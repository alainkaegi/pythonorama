# Methods
## Calling Methods
In addition to data, an object can have *methods*: things you can ask it to do. For example, `'hello'.upper()` is asking the string `'hello'`, "give me an upper-case version of yourself". It returns 
`'HELLO'`.

Similarly, `'hello'.index('e')` asks the same string, "at what position does the substring `'e'` appear within you?". The returned answer is `1`.

Calling a method is almost exactly like calling a regular function, but you have to call it *on* some particular object. Whereas a regular function call might look like `max(3, 2)`, a method call might look like `s.index('e')` (where `s` is some string). You are therefore *calling the `index` method on `s`*.

One key advantage of this approach is that different classes can have methods with the same name. For example, suppose `c` is an instance of the `Circle` class and `s` is an instance of the `Square` class. (These classes will be defined below.) Asking for `c.area()` uses `Circle`'s `area` method, while `s.area()` uses `Square`'s. This ability for the same word to mean different things in different contexts is called *polymorphism*.
## Defining Methods



## Resources
- Sedgewick and Wayne, *Introduction to Programming in Java*, [Section 3.2](https://introcs.cs.princeton.edu/java/32class/)
- Horstmann, *Core Java, Volume I: Fundamentals, 11th Edition*, Section 4.3

## Questions
1. :star: When, if ever, is an instance method declared static?
1. :star::star: Is `this` a reserved word? What about `that`?
1. :star::star: When, if ever, is `this == null`?
1. :star::star: Add a method `perimeter`, which takes no arguments and returns the Square's perimeter, to the class below.
    ```java
    class Square {

        double side;

        Square(double s) {
            side = s;
        }

    }
    ```
1. :star::star: Supply the missing line in the class below.
    ```java
    class Snake {

        Snake(double length) {
            this.length = length;
        }

        double getLength() {
            return length;
        }

    }    
    ```
1. :star::star: Why does the class below not compile?
    ```java
    class Account {

        int balance;

        int getBalance() {
            return balance;
        }

        static void main(String[] args) {
            System.out.println(getBalance());
        }

    }
    ```
1. :star::star: By adding an instance variable, modify the class below so that the instance methods don't need arguments.
    ```java
    class Square {

        public static void main(String[] args) {
            Square s = new Square();
            double side = 3;
            System.out.println("Area: " + s.area(side));
            System.out.println("Perimeter: " + s.perimeter(side));
        }

        double area(double side) {
            return side * side;
        }

        double perimeter(double side) {
            return side * 4;
        }

    }
    ```
## Answers
1. Never. By definition, an instance method is one that is *not* declared static.
1. `this` is a [reserved word](https://en.wikipedia.org/wiki/List_of_Java_keywords). `that` is not, but it is sometimes a reasonable name for a parameter of the same type as `this`.
1. Never. Calling an instance method on `null` results in a `NullPointerException`. 
1.
    ```java
    double perimeter() {
        return 4 * side;
    }
    ```
1. The line
    ```java
    double length;
    ```
    should be added inside the class (but not inside any method).
1. The instance method `getBalance` cannot be called from the static method `main`. It would work to print `new Account().getBalance()`.

1.
    ```java
    class Square {

        double side;

        public static void main(String[] args) {
            Square s = new Square(3);
            System.out.println("Area: " + s.area());
            System.out.println("Perimeter: " + s.perimeter());
        }

        Square(double side) {
            this.side = side;
        }

        double area() {
            return side * side;
        }

        double perimeter() {
            return side * 4;
        }

    }
    ```
