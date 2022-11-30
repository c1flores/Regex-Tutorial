# Regex Tutorial

This tutorial seeks to define a regular expression in programming contexts, 
commonly known as regex. A regex is a sequence of characters that defines a specific search pattern. 
When included in code or search algorithms, regular expressions can be used to find certain 
patterns of characters within a string, or to find and replace a character or sequence of characters 
within a string. They are also frequently used to validate input.

## Summary
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

An example of a regex can be seen above. For the purpose of this tutorial, we will be looking at a sequence 
of characters that can be used as a regex to search for most URLs, with the exception of some edge cases. The tutorial will break down 
the components of the "Matching a URL" regex to explore regex components in general. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)

## Regex Components

### Anchors
Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:
- ```^``` – The caret anchor matches the beginning of the text. Specifically, it signifies a string that begins with the characters that follow it. This includes an exact string match, such as ```^The``` where the strings ```The``` or ```The person``` match, but ```the``` and ```the person``` do not. This is because regex is case-sensitive. 

- ```$``` – The dollar anchor matches the end of the text. It signifies a string that ends with the characters that precede it. Similar to the caret ```^``` anchor, it can be preceded by an exact string or a range of possible matches. 

In our "Matching a URL" regex, the string must start and end with something that conforms to the patterns defined between ```^``` and ```$```.

### Quantifiers
Quantifiers are how we read occurrences of certain patterns or characters in a regex. They can be appended at the end of any character, string, or pattern. Quantifiers are inherently greedy, meaning they match as many occurrences of particular patterns as possible. They include the following:
- ```*``` - Matches the pattern zero or more times.
- ```+``` - Matches the pattern one or more times.
- ```?``` - Matches the pattern zero or one time.
- ```{}``` - Curly brackets can provide three different ways to set limits for a match:
  - ```{ n }``` - Matches the pattern exactly ```n``` number of times.
  - ```{ n, }``` - Matches the pattern pattern at least ```n``` number of times.
  - ```{ n, x }``` - Matches the pattern from a minimum of ```n``` number of times to a maximum of ```x``` number of times.
  
 Each of these quantifiers can be made lazy by adding the ```?``` symbol after it, meaning it will match as few occurrences as possible. 
 
 In our "Matching a URL" regex, the following quantifiers are used in the following instances:
 - The initial ```https``` component: 
  ```
  (https?:\/\/)?
  ```
  This grouping contains two ```?``` quantifiers. This expression is looking for an ```http://``` or an ```https://```. A *single* ```s``` is optional. The same is true for the entire expression included in the parenthesis, which explains why the grouping is followed by a ```?```. Therefore, a valid URL may begin with ```http://``` or ```https://```, or it may not begin with either of them at all (the input might begin with ```www.```). The same applies for the ```/``` at the tail end of that grouping. 
  
 - The domain name: 
 ```
 ([\da-z\.-]+)\.
 ```
 
 - The top-level domain: 
 ```
 ([a-z\.}{2,6})
 ```
 
 - The file path:
 ```
 ([\/w \.-]*)*
 ```

### Character Classes

### Flags

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

## Author

Christian Flores is a student of the Coding Bootcamp with the University of California, Berkeley. 
To see more of his work visit his [GitHub Profile](https://github.com/c1flores)
