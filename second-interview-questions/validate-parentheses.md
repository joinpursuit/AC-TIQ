# Validate Parentheses


## Prompt

Write a parentheses, brackets, and braces validator.
It should take in a String and consider the _openers_ and _closers_ that
appear within it.

_Openers_ are `'(', '[', '{'`.

_Closers_ are `')', ']', '}'`.

Write an efficient function that determines if the input String's openers
and closers are properly matched and nested.

## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:
* Should the return type be a boolean? _Yes_
* Could the input String ever be null or empty? _Yes; in that case return true_
* What should we do with non-opener or closer characters? _Ignore them_


## Sample Inputs & Outputs

| Input | Output |
|---|---|
| "{ [  ] (  )  }" | true |
| "{ [ }" | false |
| "{ [ ( ] ) }" |  false |
| "" | true |


## Hints

If a fellow has been stuck for several minutes,
it's OK to offer a hint to keep things moving:
* If they really don't know where to begin, ask how they might be able to look at each character in the string one at a time. (i.e. iterate over it with a loop)
* If they don't know what to do inside the loop, ask what it is that we want to determine about each character (i.e. is it an opener? is it a closer?)
* If they don't know how to store the openers they find, ask them if there is a data structure that would provide easy access to the last item that was added (i.e. stack)
* If their function is getting unreadable with so many conditional expressions, remind them it's OK to write and use helper methods like `isOpener()` or `isCloser()` (though this is not required!)


## Solution Overview

General steps:
* Declare an empty stack
* Loop through the input String
* For each character:
  * If it's an opener, push it onto the stack
  * If it's a closer, pop the most recent opener from the stack and check if it matches this closer
    * If it doesn't match, return false
* If you get thru the whole loop without returning false, then return true


## Solution Code

```javascript
// Javascript
function validParentheses(str) {
    if (str === null || str.length === 0) {
        return true;
    }
  
    var stack = [];
    
    for (var i = 0; i < str.length; i++) {
        if (isOpener(str[i])) {
            stack.push(str[i]);
        } else if (isCloser(str[i])) {
            if (getMatchingOpener(str[i]) !== stack.pop()) {
                return false;
            }
        }
    }
    return true;
}

function isOpener(char) {
    return char === '(' || char === '[' || char === '{';
}

function isCloser(char) {
    return char === ')' || char === ']' || char === '}';
}

function getMatchingOpener(char) {
    switch (char) {
        case ')': return '(';
        case ']': return '[';
        case '}': return '{';
        default: return null;
    }
}
```