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
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)

## Regex Components

### Anchors

Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:
- ```^``` – The caret anchor matches the beginning of the text. Specifically, it signifies a string that begins with the characters that follow it. This includes an exact string match, such as ```^The``` where the strings ```The``` or ```The person``` match, but ```the``` and ```the person``` do not. This is because regex is case-sensitive. 

- ```$``` – The dollar anchor matches the end of the text. It signifies a string that ends with the characters that precede it. Similar to the caret ```^``` anchor, it can be preceded by an exact string or a range of possible matches. 

In our "Matching a URL" regex, the input string must start and end with something that conforms to the patterns defined between ```^``` and ```$```.

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
 
 In our "Matching a URL" regex, quantifiers are used in the following instances:
 - The initial ```https``` component: 
 
  ```
  (https?:\/\/)?
  ```
  This grouping contains two ```?``` quantifiers. This expression is looking for an ```http://``` or an ```https://```. A *single* ```s``` is optional. The same is true for the entire expression included in the parenthesis, which explains why the grouping is followed by a ```?```. Therefore, a valid URL may begin with ```http://``` or ```https://```, or it may not begin with either of them at all (the input might begin with ```www.```).
  
 - The domain name ```(google or wikipedia)```: 
 ```
 ([\da-z\.-]+)\.
 ```
 This grouping contains the ```+``` quantifier. The bracket expression will accept any single digit character, any lowercase letter from a-z, or the special characters ```.``` or ```-```. The ```+``` quantifier indicates that the pattern must match 1 or more times. 
 
 - The top-level domain ```(.com, .org, .etc)```: 
 ```
 ([a-z\.]{2,6})
 ```
 This grouping contains the ``` { 2, 6}``` quantifier. This is used to signify that the pattern must match a minimum of 2 and a maximum of 6 times. Specifically, the bracket expresion indicates that any lowercase letter a-z, a slash, or a dot will produce a match. 
 
 - The file path or endpoint ```(/home, /about, /etc)``` :
 ```
 ([\/\w \.-]*)*
 ```
 This expression signifies that the expression ```[\/\w \.-]``` may match 0 or more times and that ```([a-z\.]{2,6})([\/\w \.-]*)``` may also match 0 or more times. In the former case, a forrward slash, any alphanumeric character from the latin alphabet, a space, a dot or dash will produce a match. Alternatively in the latter case, a file or endpoint may not match at all (the URL can be a plain domain). 

### Character Classes

A character class in a regex defines a set of characters which can occur in an input string to produce a match. Bracket expressions, as seen in the following examples from our URL regex, ```[\da-z\.-]```  ```[a-z\.]``` ```[\/\w \.-]```, are a type of character class. Here are some other common character classes:

- ```.``` - Matches any character expect the newline charcter (```\n```).
- ```\d``` - Matches any Arabic numeral digit. This class is equivalent to the bracket expression ```[0-9]```.
- ```\w``` - Matches any alphanumeric character from the basic Latin alphabet, including the underscore (```_```). This class is equivalent to the bracket expression ```[A-Za-z0-9_]```.
- ```\s``` - Matches a single whitespace character, including tabs and line breaks. 

Each of the last three character classes aforementioned can be changed to perform an *inverse match* by capitalizing the letter character. For example, ```\D``` matches a non-digit character.

In our URL regex, we see the  ```\d``` and ```\w``` character classes applied in the following ways, each instance used inside a bracket expression:

- The single digit character class ```\d```
```
[\da-z\.-]
```
This expression will accept any single digit character, any lowercase letter from ```a-z```, or the character ```,``` or ```-```.

- The alphnumeric character class ```\w```
```
[\/\w \.-]
```
This expression will accept the character ```/```, any word character, space, or the character ```.``` or ```-```.

It is important to note that ```.``` denotes a mach for wildcard characters, the ```\.``` seen in the expressions above are looking for the ```.``` charcater explicitly, and not the character class. 

### Grouping and Capturing
While our "Matching a URL" regex is fairly straightforward, Regular expresions can quicKly grow more complicated in an effort to check multiple parts of a string to determine that different sections fulfill different requirements. To break these sections up and **capture** certain patterns, we can use **grouping** constructs. 

The primary way of capturing a certain pattern is by surrounding the expression we wish to capture in parentheses like this: ```/(...)/```. Grouping constructs are powerful becuase they allow us to concatenate patterns or append a quantifier to a group instead of a singular character.

### Bracket Expressions

### Greedy and Lazy Match

## Author

Christian Flores is a student of the Coding Bootcamp with the University of California, Berkeley. 
To see more of his work visit his [GitHub Profile](https://github.com/c1flores)
