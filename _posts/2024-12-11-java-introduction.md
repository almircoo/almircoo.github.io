---
title: Java Introducction
date: 2024-12-11 12:00:00 +05:30
categories: [Java, Introduction]
tags: [Java]     # TAG names should always be lowercase
---
ava is a general-purpose, OOP language designed with the idea of Write Once, Run Anywhere (WORA), meaning that the Java code would work virtually in every computer without the need of re-compilation like C or C++. In order to obtain this unique portability, the computer needs to have the JVM (Java Virtual Machine) installed. Nowadays, Java is the most used programming language in the world, used for almost anything, from embedded programming to large software development, web application development and supercomputers. Java has 3 main implementation named Java EE, Java SE and Java ME meaning respectively Java Enterprise Edition, Java Standard Edition and Java Micro Edition (used in the abbreviated form as J2EE, J2SE and J2ME). Java, firstly developed at Sun Microsystems which merged into Oracle Corporation, was designed with 5 main principles in mind:

> **Terminology Note**
>
> A **program** may refer to something that can be readily run/executed (such as an application software), or it may refer to the entire "source code" that the application is generated from. **Source Code** refers to the human-readable form of the program that is written in a programming language such as Java. "Source code" is often shortened to just "code", although "code" often refers to smaller parts of the complete source code.
>
> In short, "program", "source code" and "code" are very related terms, and for our purposes, we might use them interchangeably.

## First Program

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

This might be one of the simplest programs you can write in Java. For now, just focus on the name `main` and the line that follows. Program execution starts at the first line following the open curly brackets `{` after `main` and ends at its matching close curly brackets `}`. Here, there's only one line within those curly brackets-pair which will be executed when the program is run. When program execution reaches that line, it will "print" (displays onto screen a.k.a "outputs") the value inside the parantheses that follow. Thus, our first Java program will output the following and exit (execution stops):

```bash
Hello world!
```

Let's add a similar line to our program:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        System.out.println("From the other side!!");
    }
}
```

This will produce an extra line of output:

```bash
Hello world!
From the other side!!
```

A program is executed sequentially from the top, and therefore the order of lines in output is the same as that in our program. Notice that both lines ends with a semi-colon `;`. A semi-colon denotes the end of a "statement," just like a full-stop denotes the end of a sentence in English. A **statement** is the smallest standalone element that expresses some action to be carried out (quoted from Wikipedia). So you could say that a program is roughly a collection of statements.

#### Try it yourself (1)

-   Write a program that prints your name and your friend's name in different lines.

## Storing Values

One of the most essential feature all programming languages provide is a way to store values and retrieve them. This is done via something called **variables**.

```java
public class Hello {
    public static void main(String[] args) {
        String s = "From the other side!!";
        System.out.println("Hello World!");
        System.out.println(s);
    }
}
```

The output is the same as our previous program:

```bash
Hello world!
From the other side!!
```

In the first statement, we define a variable named `s` and stores the text `"From the other side!!"` in it. In the final statement, we retrieve the value of `s` and prints it. `String` is the "type" of the variable `s` and it should match the "type" of the value being stored. **Types** are used to categorize and interpret different values. And of course `String` is the name of a type that represents text. Java has many more built-in types (e.g. `int` for integers), which we'll discuss later.

Another thing to notice here is that, in the third statement, `s` is not enclosed in double-quotes. Anything enclosed in double-quotes is treated as a `String` value. Thus if the last statement were `System.out.println("s");` then it would simply output the letter `s` and not the value stored in the variable named `s`. And conversely, if the second statement were `System.out.println(Hello world!);` without double quotes, our program would not compile since the compiler would try looking for a variable named `Hello world` which is not defined, and `!` will be treated as an operator but it is used incorrectly.

As we mentioned before, since the execution is sequential, the following program is *invalid*:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        System.out.println(s);
        String s = "From the other side!!";
    }
}
```

The above program is invalid because the variable `s` is used *before* it is defined.

We can also change the value stored in a variable:

```java
public class Hello {
    public static void main(String[] args) {
        String s = "Hello world!";
        System.out.println(s);
        s = "From the other side!!";
        System.out.println(s);
    }
}
```

Notice that the third statement that changes the value of `s` is different from the first statement which defines `s` --- it doesn't specify the type `String`. This is by design: We *must* specify the type of a variable once, and only once, which must precede all uses of that variable. Consequently, a variable cannot change the type of value it stores. The first statement, where the type of a newly introduced variable `s` is specified, is called a **variable declaration statement**. And the third statement, where a new value is given (assigned) to it, is called an **assignment statement**.

Here's an example involving a numeric typed variable:

```java
public class Hello {
    public static void main(String[] args) {
        int lucky = 8;
        System.out.println("Here's a number:");
        System.out.println(lucky);
        System.out.println("Can you multiply it by twelve?");
        lucky = lucky * 12;
        System.out.println(lucky);
        System.out.println("Ain't that great?!");
    }
}
```

Here's the output:
```bash
Here's a number:
8
Can you multiply it by twelve?
96
Ain't that great?!
```

Here, we create a variable named `lucky` having type `int` to store an integer. We later modify its value to multiply its value with 12, before printing it again. Note that in an assignment statement, the expression on the right of `=` is evaluated and gets assigned to the variable on the left. So unlike in maths, this is not an assertion of equality, and the order matters. Thus the following statements are both *invalid*:

```bash
60 = lucky;
lucky * 12 = lucky;
```

#### Try it yourself (2)

-   Write the output of the following program:
    ```java
    public class Hello {
        public static void main(String[] args) {
            String x = "Hello Neo!";
            String y = "You are The One.";
            x = "Wanna hang out sometime?";
            System.out.println(y);
        }
    }
    ```
-   Are there any errors in the following program? Correct them, if any:
    ```java
    public class Hello {
        public static void main(String[] args) {
            int hi = "1234";
            System.out.println(hi);
        }
    }
    ```

## User Input

User interaction is essential to make things interesting. Let's see how a basic interaction can be set up.

```java
import java.util.Scanner;

public class Hello {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.println("Enter 2 numbers:");
        int a = s.nextInt();
        int b = s.nextInt();
        System.out.println("Here's their sum:");
        System.out.println(a + b);
    }
}
```

That's a lot to take in at once. Let's break it down line-by-line:

```java
import java.util.Scanner;
```

The first line is called an **import statement**, which is used to bring extra features to our program. In this case, it tells the compiler that we are going to use a type called `Scanner` which is part of an optional package that is bundled with the Java compiler. `Scanner` provides a bunch of "methods" that can make it easier to work with user input (we'll look into "why" and "how" parts of it later).

```java
Scanner s = new Scanner(System.in);
```

This statement defines a variable named `s` and assigns a "new `Scanner` object" to it. Notice the `System.in` part --- this specifies that the `Scanner` object must be created to work on `System.in`. So what is `System.in`? Up till this point, notice how we were displaying outputs --- we were calling the `println` "method" of `System.out`. Yes, you are correct in guessing that `System.out` is for showing the user some output, and `System.in` is for taking some input from the user. Thus the above statement creates a new `Scanner` object which works on the user input. (Also yes, `Scanner` objects can be created to work on things other than user input; such as files, network stream etc.)

> #### Sidenote: Methods
>
> A **method** is roughly a named collection of statements. And a **method call** (using that name) will execute those statements, while optionally taking in one or more values (called **arguments**) and producing some value (called **return value**). So far we have seen `println` method of `System.out` object, and `nextInt` method of a `Scanner` object. `println` takes a single argument and returns nothing (technically, `void`). `nextInt` takes no arguments and returns an integer value. If all this sounds confusing right now, don't worry, we'll discuss this in more detail later.

```java
int a = s.nextInt();
int b = s.nextInt();
```

Both these statements is asking the `Scanner` object `s` to try to extract an integer value from its underlying "stream" (`System.in` --- user input). This will make the program to wait for user input, and if the user inputs an integer and presses enter, it will get stored in variable `a` and the program will wait again for user input, this time to be stored in variable `b`.

> **Sidenote:** The user input stream, `System.in`, is actually a stream of text, and if we provide non-numeric input when `nextInt` method of `Scanner` was called, the `Scanner` will throw an error and abort the program.

#### Try it yourself (3)

-   What would the above program output if the user enters `40` and then `50`? 
-   Write a program that takes a number as user input, multiplies it by `1024` and prints the result.

## Logic and Flow Control

Java has a type called `boolean` to work with logic. Here's an example to show you what that means:

```java
public class Hello {
    public static void main(String[] args) {
        boolean isGreat = 5 > 4;
        System.out.println("Is five greater than four?");
        System.out.println(isGreat);
        System.out.println("Is eight less than three?");
        System.out.println(8 < 3);
        System.out.println("Are you doing great today?");
        isGreat = true;
        System.out.println(isGreat);
    }
}
```

The above program will produce the following output:

```bash
Is five greater than four?
true
Is eight less than three?
false
Are you doing great today?
true
```

Let's break this program down.

```java
boolean isGreat = 5 > 4;
```

As you know, this is a declaration statement that introduces a `boolean`-typed variable named `isGreat` and assigns a value to it. A `boolean` variable can take one of two values: `true` or `false`. In this case, the value is the result of evaluating expression `5 > 4`. Technically speaking, the greater-than operator `>` takes two numeric operands and evaluates to a boolean value --- `true` if the left operand is greater than the right one and `false` otherwise. Therefore `5 > 4` evaluates to `true`, and that value is assigned to the variable.

```java
System.out.println(8 < 3);
```

Here, the value obtained by evaluating the expression `8 < 3` will get printed. Like before, the less-than operator also evaluates to a boolean value, and in this case, `8 < 3` evaluates to `false`.

```java
isGreat = true;
```

Here, we are directly assigning a boolean value to the variable.

#### Try it yourself (4)

-   Write the output of the following program:
    ```java
    public class Hello {
        public static void main(String[] args) {
            System.out.println("Is it true that cats eat mouse?");
            System.out.println(12 < 0);
        }
    }
    ```

### Relational Operators

Here's a list of all relational operators in Java.

| Operator |           Name           |       Comments       |
|----------|--------------------------|----------------------|
| `>`      | Greater than             | `4 > 4` is `false`.  |
| `<`      | Less than                | `3 < 4` is `true`.   |
| `>=`     | Greater than or equal to | `4 >= 4` is `true`.  |
| `<=`     | Less than or equal to    | `3 <= 4` is `true`.  |
| `==`     | Equal to                 | `3 == 4` is `false`. |
| `!=`     | Not equal to             | `3 != 4` is `true`.  |

### Simple Branching

With the help of booleans, Java provides a mechanism to conditionally execute a bunch of statements. Here's an example:

```java
public class Hello {
    public static void main(String[] args) {
        int marks = 80;
        if (marks > 60) {
            System.out.println("Wow, that's great!");
        } else {
            System.out.println("Better luck next time!");
        }
    }
}
```

The above program will generate the following output:

```bash
Wow, that's great!
```

This is an example of an `if`-statement. To see how it works, let's start with the basic syntax:

```java
if (condition) {
    statement1;
} else {
    statement2;
}
```

Here, `condition` is a placeholder for an expression that *must* evaluate to a boolean value. If `condition` evaluates to `true`, everything within the first curly brackets gets executed (i.e. `statement1;`), otherwise if `condition` evaluates to `false`, everything within the curly brackets following `else` gets executed (i.e. `statement2;`).

So, back to our example, since `marks > 60` evaluates to `true`, only the first print-statement will be executed and the `else`-part will be skipped.

> **Sidenote:** This is called a "branching construct" because, if you look at the flow diagram below, you'll see that the program selects a "branch" based on a condition:
>
> ![if-then-else-flow](http://svgur.com/i/3T2.svg)

I should also note that specifying the `else`-part is optional. So the following is also syntactically valid:

```java
if (condition) {
    statement1;
}
```

In this case, if the `condition` turned out to be `false`, the program execution simply skips over whatever is in those curly brackets (i.e. `statement1;` will be skipped).

#### Try it yourself (5)

-   Write a program that asks the user to enter a number, and prints `Negative` if the number was less than zero, and prints `Positive` otherwise.
-   Write the output of the following program:
    ```java
    public class Hello {
        public static void main(String[] args) {
            boolean b = false;
            if (b) {
                System.out.println("Ninja");
            } else {
                System.out.println("Kitty");
            }
        }
    }
    ```

## Comments

When writing a program, it is often useful to include a summary of what a piece of code does along with the code itself, and it is referred to as **comments**. Java has a specific syntax for writing comments so that it is ignored by the compiler during the compilation process. Below is an example of using **inline comments**:

```java
// this is some comments about this great class!
public class Hello {
    // here is another comment
    public static void main(String[] args) { // you may not like it but
        System.out.println("Hello"); // the compiler happily ignores all this
    }
} // more comments to annoy you!
```

The above program compiles fine and simply outputs `Hello`. In a line, if the compiler encounters two forward-slashes `//` (without space in between), it ignores all text that follows within that line.

## Numbers and Arithmetic

Now, let's do some math!

```java
public class Hello {
    public static void main(String[] args) {
        int sum = 50 + 20;
        int diff = 50 - 20;
        int prod = 50 * 20;
        int quot = 50 / 20;
        int remd = 50 % 20;
        System.out.println(sum); // prints 70
        System.out.println(diff); // prints 30
        System.out.println(prod); // prints 1000
        System.out.println(quot); // prints 2
        System.out.println(remd); // prints 10
        System.out.println("Look ma! The computer does math!!");
    }
}
```

The output of each line is mentioned in comments. The variable names stand for sum, difference, product, quotient and reminder respectively (in order from top). Percent-symbol `%` is called the **modulus operator** where `x % y` evaluates to the reminder when `x` is divided by `y`. So `50 % 20` will evaluate to `10` since `50 = 20 * 2 + 10`. Also note that `50 / 20` evaluates to `2` (the quotient part in the equation: `50 = 20 * quot + remd`). There's another reason why Java works this way --- the `int` type can only store integers. We use another type for real numbers.

Introducing floating point numbers:

```java
public class Hello {
    public static void main(String[] args) {
        double quot = 50.0 / 20.0;
        System.out.println(quot); // prints 2.5
        System.out.println("Yeah!");
    }
}
```

Here, `double` stands for "double-precision floating-point numbers." And **floating-point numbers** is simply a representation of real numbers with limited precision (significant digits) (more on that later). One important thing to note here is that `50 / 20` is not the same as `50.0 / 20.0`, because in the former, an integer division is performed (giving a result of `2`), while in the latter, a floating point division is performed (regardless of how the result is consumed). This is in turn due to `50` and `20` being given the type `int`, whereas `50.0` and `20.0` are given the type `double`.

```java
public class Hello {
    public static void main(String[] args) {
        double quot = 50 / 20;
        System.out.println(quot); // prints 2.0
        System.out.println("Got it?");
    }
}
```

Even though the type of the variable `quot` is `double`, the evaluation of `50 / 20` is not affected by it, and consequently only an integral division is performed. The resulting integer `2` is converted to a `double` and stored in the variable `quot`. We'll discuss more about numeric representations and type conversions later.

#### Try it yourself (6)

- Write a program that takes a number from the user and checks whether it is divisible by 12. (Hint: Use modulus operator, and an `if`-statement)

### Order of Evaluation