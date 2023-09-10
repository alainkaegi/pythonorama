# Operators
## Overview
*Operators* are used to combine expressions (such as [literals](data_structures/built_in_types.md#Literals)) into larger expressions. For example, in `2 + 3`, the `+` operator combines the two operands `2` and `3` into a larger expression which evaluates to the value of 5.

*Binary operators*, like `+`, are *infix*, meaning that they appear between their two operands. *Unary operators*, like `-` when it is used for negation rather than subtraction, are *prefix* if they appear before the operand and *postfix* if they appear afterward. There is one *ternary operator*, conditional expression A if C else B, which takes three arguments, `A` before the `else`, `C` between the `if` and `else`, and `B` after the `else`.

The operators are summarized in the table below. See the additional resources for more information.

Category|Operators|Notes
-|-|-
Arithmetic|`+ - * / // % **`|`/` is the division operator.<br>`//` is the floored division.<br>`%` is the remainder operator, sometimes called the modulo operator.<br>`**` is the exponentiation operator.<br>`-` can be used for negation (prefix) or subtraction (infix).
Comparison|`< <= == >= > !=`<br>`[not] in`<br>`is [not]`|These operators evaluates to boolean values.<br>`!=` means "is not equal to".<br>`x in s` returns `True` if `x` is a member of `s`.<br>`x is y` return `True` if and only if `x` and `y` are the same object.
Assignment|`= += -= *= /= //= %= **= <<= >>= &= ^= \|=`|Assignments are also statements.<br>`x += 5` roughly means `x = x + 5`.
Logical|`and or not`|These take boolean operands and produce boolean values.<br>`and` and `or` are short-circuited.<br>`not` is prefix.
Bitwise|`& \| ~ ^ << >>`|These operate on integer types.<br>`~` and `^` are prefix.
Conditional|`if else`|`A if C else B` has the value of `A` if `C` is true, `B` otherwise.
Concatenation|`+`|`s1 + s2` is the concatenation of strings `s1` and `s2`.

## Operator Precedence
In an expression involving multiple operators, like `2 + 3 * 4`, *operator precedence* rules determine the order in which operations are carried out. In this case, multiplication has higher precedence than addition, so the multiplication happens first, giving a result of 14.

Like almost all modern languages, Python has an elaborate [operator precedence hierarchy](https://introcs.cs.princeton.edu/python/appendix_precedence/). You will gain some intuition about it with practice, but you are not expected to memorize it. If there is every any doubt, use parentheses to clarify order of operations. For example, you might write the expression above as `2 + (3 * 4)`. 

## Resources
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.2](https://introcs.cs.princeton.edu/python/12types/)
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Appendix A: Python Operator Precedence](https://introcs.cs.princeton.edu/python/appendix_precedence/)
- Python official documentation, The Python Language Reference, [Expressions](https://docs.python.org/3/reference/expressions.html)
- Anderson, [Bit Twiddling Hacks](https://graphics.stanford.edu/~seander/bithacks.html) (These are in C, but the operators are pretty much the same in C and in Java.)

## Questions
1. :star: What is the value of `1 + 2`
1. :star: What is the value of `'1' + '2'`
1. :star: What is the value of `5 - 2 * 3`?
1. :star: What is the value of `83 % 10`?
1. :star::star: `x << 1` is the same what common arithmetic operation?
1. :star::star: What is the value of `5 / 3`?
1. :star::star: What is the value of `5 // 3`?
1. :star::star: What is the value of `-1**2`?
1. :star::star: What is the value of `1/0`?
1. :star::star: A set of numbers represented as an `int`. Suppose `a` and `b` are two such sets. What Java expression produces the intersection of these two sets?
1. :star::star: Suppose the binary representation of `a` is `1100` and the binary representation of `b` is `1010`. What is the binary representation of `a ^ b`?
1. :star::star::star: What is the value of `-32 % 10`?

## Answers
1. The integer 3.
1. The string `'1+2'`.
1. -1, because multiplication has higher operator precedence than subtraction.
1. 3, because when 83 is divided by 10 the remainder is 3.
1. Multiplying by 2.
1. 1.6666666666666667, because `/` is the division operator.
1. 1, because `//` is the floored division operator.
1. -1, because `**` has higher precedence than the unary `-` operator.
1. No value is produced, instead Python raises a ZeroDivisionError at run time.
1. `a & b`.
1. `0110`.
1. 8, the result of `%` is never negative, even if the first argument to `%` is negative. This is consistent with the interpretation of `%` as "modulo" but not really with the interpretation as "remainder".
