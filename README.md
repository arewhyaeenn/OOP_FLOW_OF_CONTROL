# COMP 150 Lab 4 - Flow of Control
In this lab:

* What boolean expressions are, and how to write and evaluate them.
* How to use `if`/`else` statements to decide what actions to take.
* How to use `for`, `while`, and `do while` loops to repeat actions.
* How to use the `break` and `continue` keywords.
* How to use a `switch`.

## Boolean Expressions

Recall that an **expression** is a combination of variables, operations and values that yields a resulting value, and that the primitive data type `boolean` stores **truth values** (`true` or `false`).

A **boolean expression** is an expression which evaluates to a `boolean` value of `true` or `false`.

The simplest boolean expressions are the `boolean` literal values themselves, `true` and `false`. Next in line are the identifiers of `boolean` variables, which evaluate to the value of said variables.

### Relational Operators

Java includes **relational operators** which return `true` or `false` depending on the values of their operands:

**OPERATOR** | **SAMPLE EXPRESSION** | **VALUE**
:----------: | :-------------------: | :-------:
`<`          | `x < y`               | `true` if `x` is less than `y`; `false` otherwise
`<=`         | `x <= y`              | `true` if `x` is less than or equal to `y`; `false` otherwise
`==`         | `x == y`              | `true` if `x` equals `y`; `false` otherwise
`!=`         | `x != y`              | `true` if `x` does not equal `y`; `false` if `x` does equal `y`
`>=`         | `x >= y`              | `true` if `x` is greater than or equal to `y`; `false` otherwise
`>`          | `x > y`               | `true` if `x` is greater than `y`; `false` otherwise

[EXERCISE] comparisons

### Boolean Operators

Java also includes **boolean operators**, which allow calculation of `boolean` values using boolean logic. Each boolean operator takes boolean expressions as operands, and outputs a boolean value based on the values of those expressions. In the following table, `a` and `b` are both assumed to be placeholders for boolean values or for boolean expressions.

**OPERATOR** | **MEANING** | **SAMPLE EXPRESSION** | **VALUE**
:----------: | :---------: | :-------------------: | :-------:
`&&`         | *and*       | `a && b`              | `true` if `a` and `b` are both `true`; `false` otherwise
`||`         | *or*        | `a || b`              | `false` if `a` and `b` are both `false`; `true` otherwise
`!`          | *not*       | `!a`                  | `true` if `a` is `false`; `false` if `a` is `true`

If you refer to the [Java 8 operator precedence](https://github.com/arewhyaeenn/COMP_150_LAB_2_JAVA_FUNDAMENTALS/blob/master/figures/operatorPrecedence.png) you'll see that, when evalutating logical expressions, first *not* operations (`!`) are performed from right to left, then *and* (`&&`) operations from left to right, and finally *or* (`||`) from left to right. Of course, parenthesis can be used to specify a different order.

Boolean operations occur after arithmetic and comparison operations.

[EXERCISE] boolean operations on `boolean` literals and `boolean` variables

[EXERCISE] boolean operations with relational operators

### Short Circuit Evaluation

When boolean operations are evaluated, the values of input expressions are only calculated if necessary; unnecessary evaluations are skipped. For instance, in the expression `a && b`, if `a` is `false` then `b` won't be evaluated because `a && b` is necessarily `false` regardless of `b`'s value. Similarly, when evaluating `a || b` if `a` is `true` then `b`'s value isn't needed to determine that `a || b` is `true`.

[EXERCISE] Follow operator precedence, show step by step evaluation of boolean expressions using arithmetic, comparison and boolean operators.

## `if`/`else`

`if` and `else` statements can be used together with boolean expressions to select which blocks to run. We'll start our discussion of `if` and `else` with an example:

```java
import java.util.Scanner;

class MyClass
{
	public static void main(String[] args)
	{
		Scanner scan = new Scanner( System.in );
		
		System.out.println("Enter an integer : ")
		long userInput = scan.nextLong();
		
		if (userInput > 10)
		{
			System.out.println("Your input was greater than 10.");
		}
		else
		{
			System.out.println("Your input was not greater than 10.");
		}
	}
}
```

The program above prompts the user for an integer, and stores their response in a variable called `userInput`. It then prints out a message, telling the user whether their input was greater than `10` or not.

[EXERCISE] Edit the program above to tell the user whether their response equals `10`.

[EXERCISE] If the two printed `String`s above are switched, what happens?

###<a name="if"></a>`if` Statements

The simplest `if` statements look like: `if ( <boolean_expression> ) { <true_block> }`.

If the boolean expression in the parenthesis is true, then the statements in the true block are executed; otherwise they are not. In the snippet below, `x` has value `5`. So, when the `if` statement's boolean expression, `x == 5`, is evaluated, it evaluates to `true`. Because the boolean expression is true, the print statement in the true block runs.

```java
int x = 5;
if (x == 5)
{
	System.out.println("mmhmmm");
}
```

If the boolean expression is `false`, then the true block does not run. The program below does not print anything to the console:

```java
int x = 6;
if (x == 5)
{
	System.out.println("mmhmmm");
}
```

### `if`/`else` Statements

An `if` statement can include a second block, called the `else` block, with instructions to execute if the boolean expression is `false`:

```java
if ( <boolean_expression> )
{
	<true_block>
}
else
{
	<false_block>
}
```

The `else` keyword precedes the false block, i.e. the instructions to execute if the boolean expression is `false`. We can expand the example `if` statement above to include an `else`:

```java
int x = <int_literal>;
if (x == 5)
{
	System.out.println("mmhmmm");
}
else
{
	System.out.println("nuh uh");
}
```

Here if the value assigned to `x` is `5`, then the message "mmhmmm" is printed; otherwise "nuh uh" is printed.

In an `if` statement, the block(s) which may or may not be executed depending on the value(s) of boolean expression(s) are called **conditional blocks**. This is because they are blocks whose contained instructions are only executed if specific conditions (specifically, those defined in the boolean expression) are met.

[EXERCISE] simple boolean, complex body

[EXERCISE] complex boolean, simple body

### Statement Nestability

If statements are structured and interpreted in the following form: `if ( <boolean_expression> ) <statement> else <statement>`.

As shown above, the trailing `else <statement>` is optional. Recall that a block can be used wherever a statement can; in the examples above, the two `<statement>`s were blocks.

Because `if` statements are a type of statement, the `<statement>` slots above could be `if` statements. In other words, `if` statements are **nestable**; one `if` statement can be a part of (i.e. can be **nested in**) another `if` statement. This means that chains of `if` statements can be made as described in the next section.

### `if`/`else if`/`else` Chains

When the `<statement>` trailing the `else` keyword is, itself, an `if` statement, you end up with something like this:

```java
if ( <boolean_expression> )
{
	...
}
else if ( <boolean_expression> )
{
	...
}
else
{
	...
}
```

Consider executing a program like the one above. If the first boolean expression is `true`, then the first block is entered and executed. Then, an `else` is reached, but because the corresponding `if`'s boolean expression was `true`, the `<statement>` trailing the `else` is not executed. In the program above, this `<statement>` is an `if` statement with an `else` of its own, all of which is not executed.

In other words, in a chain of `if`/`else if` statements, only one `true` block will be entered.

Consider this example:

```java
import java.util.Scanner;

class DoorGuard
{
    static String CURRENT_PASSWORD = "password123";
    static String OLD_PASSWORD = "password";

    public static void main(String[] args)
    {
        Scanner keyboard = new Scanner( System.in );
        System.out.println("What's the password?");
        String userResponse = keyboard.next();

        if ( userResponse.equals(CURRENT_PASSWORD) )
        {
            System.out.println("Welcome back!");
        }
        else if ( userResponse.equals(OLD_PASSWORD) )
        {
            System.out.println("That's the old password...");
        }
        else
        {
            System.out.println("Get lost!");
        }
    }
}
```

Notice that the boolean expressions above don't use the relational operators; the instead make calls to the `userResponse` `String`'s `equals` method. This is because `String`s are objects, not primitives, so the `==` operator would check if they are the **same object** (i.e. if they reference the same location in memory); we want to check if they contain the same characters, which is defined in the `String` class's `equals` method. We will discuss this in much more detail in the next lab; for now just know that the `String.equals` method compares two `String`s and returns `true` if they contain the same sequence of characters.

[EXERCISE] What happens if the user enters the current password in the example above? What if they enter the old password? What if they enter something else entirely?

[EXERCISE] Go on an if-else flow adventure with the debugger.

### `if` Statements, Blocks, and Nestability

The conditional blocks in `if` statements are, well, blocks; they can contain a sequence of statements. These contained statements can also be `if` statements (or any other type of statement). For example, the program below consists of an `if` statement whose conditional blocks contain more `if` statements.

```java
import java.util.Scanner;

class FreeJacket
{
    final static String YES_RESPONSE = "yes";
    final static String NO_RESPONSE = "no";

    public static void main(String[] args)
    {
        Scanner keyboard = new Scanner( System.in );
        String userResponse;

        System.out.println("Are you cold? (yes / no)");
        userResponse = keyboard.next();

        if ( userResponse.equals(YES_RESPONSE) )
        {
            System.out.println("Would you like a FREE JACKET? (yes / no)");
            userResponse = keyboard.next();
            if ( userResponse.equals(YES_RESPONSE) )
            {
                System.out.println("Here ya go!");
            }
            else if ( userResponse.equals(NO_RESPONSE) )
            {
                System.out.println("Who likes comfort anyway?");
            }
            else
            {
                System.out.println("\"yes\" or \"no\" ... ");
            }
        }
        else if ( userResponse.equals(NO_RESPONSE) )
        {
            System.out.println("Liar! Do you want a FREE JACKET? (yes / no)");
            userResponse = keyboard.next();
            if ( userResponse.equals(YES_RESPONSE) )
            {
                System.out.println("I knew you were cold...");
            }
            else if ( userResponse.equals(NO_RESPONSE) )
            {
                System.out.println("But it's free...");
            }
            else
            {
                System.out.println("\"yes\" or \"no\" ... ");
            }
        }
        else
        {
            System.out.println("\"yes\" or \"no\" ... ");
        }
    }
}
```

[EXERCISE] Read the program above. Theorize about how it should behave. When you believe you know what it will do in any case (i.e. with any sequence of user inputs) run it to test your theory. You shoud use the debugger, so you can step through line by line and see what's happening.

[EXERCISE] Write a program to specification using nested ifs

## `while` Loops

Sometimes it is necessary to repeat an action multiple times. This can be done with a **loop**. There are several types of loops in Java. The simplest type of loop is the `while` loop. `while` loops look like this:

```java
while ( <boolean_expression> )
{
	<loop_body>
}
```

As long as the boolean expression, called the **loop condition** remains `true`, the loop will keep repeating the statements in the **loop body**. The loop essentially works as follows:

1. Evaluate the loop condition.
2. If the loop condition is `true`, execute the instructions in the loop body, then start over on step 1.
3. Otherwise, resume execution on the line after the loop body.

Each repetition of the instructions in the loop body is called an **iteration**. To **iterate** is to go through an iteration.

The snippet below should iterate 10 times; it should print out the numbers `0` through `9`.

```java
int i = 0;
while (i < 10)
{
	System.out.println(i);
	++i;
}
```

[EXERCISE] Determine what value `i` has in the snippet above after the loop ceases interation.

[EXERCISE] Create a simple program the the while loop above in its main method. Run with debugger...

[EXERCISE] Read a while loop example and answer questions about it.

[EXERCISE] Write a program involving a while loop to meet specifications.

## `do while` Loops

The `do while` loop is very similar to the `while` loop. There are two differences. The first difference is in how the loop itself is written. A `do while` loop is written like this:

```java
do {
	<loop_body>
} while ( <boolean_expression> );
```

The second difference is that the `while` loop checks the loop condition before the first iteration, where the `do while` loop does not. In other words, a `while` loop can iterate 0 times if the loop condition is initially `false`, but a `do while` loop will **always** iterate at least once.

Anything that can be done with a `do while` loop can also be done with a `while` loop. The `do while` loop above could be written identically with a `while` loop like this:

```java
<loop_body>
while ( boolean_expression )
{
	<loop_body>
}
```

Sometimes, a loop body must iterate at least once, and it is easier (more concise) to write a `do while` loop. For example, loops are often used to get valid user inputs with the following sequence of events:

* prompt the user for a response
* read the user's response
* validate the user's response (check if it is valid)
* if the user's response is invalid, start over
* if the user's response is valid, continue

Consider for example the `UserWrangler` class:

```java
/*
    The UserWrangler class will define methods to facilitate console interactions
    with the user (prompting, interpreting responses, validating responses...).
 */

import java.util.Scanner;

class UserWrangler
{
    final static String YES_RESPONSE = "yes";
    final static String NO_RESPONSE = "no";
    final static Scanner keyboard = new Scanner( System.in );

    static boolean getYesNoResponse(String prompt)
    {
        String userResponse;

        // repeatedly ask the user for a response (and tell them what their options are)
        // until that idiot figures out how to type "yes" or "no" ;)
        do {
            System.out.println(prompt + " (" + YES_RESPONSE + " / " + NO_RESPONSE + ")");
            userResponse = keyboard.next();
        } while ( !(userResponse.equals(YES_RESPONSE) || userResponse.equals(NO_RESPONSE)) );

        return userResponse.equals(YES_RESPONSE);
    }
}
```

At the moment, the class above contains a single method, called `getYesNoResponse`. It takes as an argument a `String`, storing the prompt (i.e. what to print to request information from the user). It returns a `boolean` value; `true` if the user enters "yes" and `false` if the user enters "no". It allows a programmer to ask the user a yes or no question, and be given the result as a `boolean` with a single method call.

[EXERCISE] Use the client below to step through `UserWrangler.getYesNoResponse` with the Debugger.

```java
class Client
{
    public static void main(String[] args)
    {
        boolean userYesNoResponse;

        while (true)
        {
            userYesNoResponse = UserWrangler.getYesNoResponse("ARA YA READY, KIDS!?");
            if (userYesNoResponse)
            {
                System.out.println("OOOOOOOHHHHHHHHHHH!!!!!");
            }
            else
            {
                System.out.println("oh...");
            }
        }
    }
}
```

[EXERCISE] or maybe just a paragraph, something to point out the infinite loop in the client above

[EXERCISE] rewrite the FreeJacket client above to use StringWrangler.getYesNoResponse

## `for` Loops

`for` loops are another loop variant. Anything that can be done with a `for` loop can also be done with a `while` loop, but in some circumstances `for` loops provide more concision.

`for` loops are structured as follows:

```java
for (<initializing_statement> ; <boolean_expression> ; <end_of_iteration_statement>)
{
	<loop_body>
}
```	

`for` loops function much like `while` loops do, but come with a bit more of the setup encased in the statement syntax. The three statements in the `for` loop's parenthesis are as follows:

* `<initializing_statement>` : executed before the first iteration.
* `<boolean_expression>` : evaluated before each iteration; if `true`, keep looping; if `false`, stop looping.
* `<end_of_iteration_statement>` : executed after each iteration, before evaluating the boolean expression for the next iteration.

Consider, for example, the while loop from above:

```java
int i = 0;
while (i < 10)
{
	System.out.println(i);
	++i;
}
```

A (nearly) identical `for` loop can be constructed using the same initial setup, loop condition, and end-of-loop statement:

```java
for (int i = 0; i < 10; ++i)
{
	System.out.println(i);
}
```

These two loops are identical in output; they both print the same numbers. There is a  difference, however. The `while` loop example declares `i` outside of the scope of the loop, so `i` still exists outside of the loop (it has a value of `10` when the loop completes). The `for` loop, on the other hand, declares `i` inside the scope of the loop, so `i` doesn't exist after the loop finishes iterating.

[EXERCISE] print i after the while loop, find out what happens when you try after the for loop

[EXERCISE] modify the for loop above so it behaves exactly like the while loop (i is still accessible afterwards).

## `break` and `continue`

A `break` statement can be used to stop a loop, without finishing the current iteration. Consider this snippet:

```java
int i = 0;
while (true)
{
	if (i == 10)
	{
		break;
	}
	System.out.println(i);
	++i;
}
```

Note that in the loop above, the loop condition is simply `true`. This means that, in theory, the loop could keep iterating forever. It will only stop iterating if it encounters a `break` statement or a `return` statement.

`i` starts at `0`, and is incrememented by `1` at the end of each iteration with `++i;`; eventually, it will be `10`, at which time the `if` condition `i == 10` will be `true`, and the `break;` statement will execute. When this happens, the `while` loop ceases looping without finishing the current iteration.

[EXERCISE] what is the first number printed by the loop above? what is the last? verify by running...

A `continue` statement will cause the loop to start iteration again from the beginning of the loop body if the loop condition is still `true`. In other words, the `continue` statement ends the current iteration, but allows the loop to continue onto the next iteration.

```java
int i = 0;
while (i < 10)
{
	++i;
	if (i % 2 == 0)
	{
		continue;
	}
	System.out.println(i);
}
```

The loop above starts `i` at `0` and increments `i` by `1` at the beginning of each iteration, so eventually the loop condition `i < 10` will be `false`. In each iteration, if `i` is even (i.e. if the remainder when `i` divided by `2` is `0`) after being incremented then the loop body starts over; otherwise, the loop body continues to print `i` before starting over.

[EXERCISE] What values are printed by the loop above? verify by running with the debugger!

## `switch`

`switch` statements can be used to when a `byte`, `short`, `int`, `char` or `String` expression has one of a finite number of values and the action taken that needs to be taken depends on that value.

Essentially, the `switch` takes as input an expression with one of these types, and performs the corresponding `case` associated with the expression's value.

In the following example, the `dayToInt` takes as an argument the name of a week, and outputs 1 for Sunday, 2 for Monday, etc.

```java
class DateUtils
{
    static int dayToInt(String dayName)
    {
        int dayInt;
        switch (dayName)
        {
            case "Sunday":
                dayInt = 1;
                break;
            case "Monday":
                dayInt = 2;
                break;
            case "Tuesday":
                dayInt = 3;
                break;
            case "Wednesday":
                dayInt = 4;
                break;
            case "Thursday":
                dayInt = 5;
                break;
            case "Friday":
                dayInt = 6;
                break;
            case "Saturday":
                dayInt = 7;
                break;
            default:
                dayInt = 0;
        }

        return dayInt;
    }
}
```


[EXERCISE] what does it output if the input is not the name of a day?

[EXERCISE] create a client class to test the `dayToInt` method. you should ensure that it outputs the correct value for every day of the week, and for a variety of invalid inputs.

[EXERCISE] :

* Add a `static` method to the `UserWrangler` class called `getMonthName` which
	* requires no arguments
	* prompts the user for the name of a month until the user enters a valid month name (use a loop)
	* returns the valid month name entered by the user
* Add to the `DateUtils` class. In it, create a `static` method called `monthToInt` which:
	* requires a String argument (the name of a month)
		* returns an `int` (1 for January, 2 for February, etc, 0 for invalid)
* Create a client class to test both `getMonthName` and `monthToInt` by using the output from `getMonthName` as the input for `monthToInt` and printing the resulting `int`

`switch`s also works with the accepted primitives' respective wrapper classes `Byte`, `Short`, `Integer` and `Character`, as well as with enumerated types (`enum`s) which we will discuss in a future lab.

### `switch` and `if` Statements

You've likely noticed that anything that can be done with a `switch` can also be done with an `if`/`else`. If the number of possibilities is sufficiently large, the `switch` is faster. However, each possibility in an `if`/`else` chain or a `switch` must be typed "by hand" and if that number is large enough for its effect on performance to be relevant, you should probably be organizing the selection a different way.

Generally, the decision to use a `switch` or an `if`/`else` chain comes down to readability in context and the preference of the programmer.

## Answers to Selected Exercises

# TODO

## Lab Assignment

# TODO


