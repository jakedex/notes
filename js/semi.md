# Semicolon omittance in JavaScript

- The statement has an unclosed paren, array literal, or object literal or ends in some other way that is not a valid way to end a statement. (For instance, ending with . or ,.)
- The line is -- or ++ (in which case it will decrement/increment the next token.)
- It is a for(), while(), do, if(), or else, and there is no {
- The next line starts with [, (, +, *, /, -, ,, ., or some other binary operator that can only be found between two tokens in a single expression.


