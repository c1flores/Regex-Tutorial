# Regex Tutorial

This tutorial seeks to define a regular expression in programming contexts, 
commonly known as regex. A regex is a sequence of characters that defines a specific search pattern. 
When included in code or search algorithms, regular expressions can be used to find certain 
patterns of characters within a string, or to find and replace a character or sequence of characters 
within a string. They are also frequently used to validate input.

  ## Matching a URL Example
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

An example of a regex can be seen above. For the purpose of this tutorial, we will be looking at a sequence 
of characters that can be used as a regex to search for most URLs, with the exception of some edge cases. The tutorial will break down 
 components of the "Matching a URL" example to explore regex components in general. 

## Table of Contents

- [Anchors](#anchors)
- [Character Classes](#character-classes)
- [Quantifiers](#quantifiers)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)

## Regex Components

### Anchors

Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:
- ```^``` – The caret anchor matches the beginning of the text. Specifically, it signifies a string that begins with the characters that follow it. This includes an exact string match, such as ```^The``` where the strings ```The``` or ```The person``` match, but ```the``` and ```the person``` do not. This is because regex is case-sensitive. 

- ```$``` – The dollar anchor matches the end of the text. It signifies a string that ends with the characters that precede it. Similar to the caret ```^``` anchor, it can be preceded by an exact string or a range of possible matches. 

In our "Matching a URL" regex, the input string must start and end with something that conforms to the patterns defined between ```^``` and ```$```.

### Character Classes

A character class in a regex defines a set of characters which can occur in an input string to produce a match. Bracket expressions, as seen in the following examples from our URL regex ```[\da-z\.-]```  ```[a-z\.]``` ```[\/\w \.-]```, are a type of character class. Here are some other common character classes:

- ```.``` - Matches any character except the newline charcter (```\n```).
- ```\d``` - Matches any Arabic numeral digit. This class is equivalent to the bracket expression ```[0-9]```.
- ```\w``` - Matches any word character from the basic Latin alphabet, any Arabic numeral digit, or the special character underscore (```_```). This class is equivalent to the bracket expression ```[a-zA-Z0-9_]```.
- ```\s``` - Matches a single whitespace character, including tabs and line breaks. 

Each of the last three character classes aforementioned can be changed to perform an *inverse match* by capitalizing the letter character. For example, ```\D``` matches a non-digit character.

In our URL regex, we see the  ```\d``` and ```\w``` character classes applied in the following ways, each instance used inside a bracket expression:

- The single digit character class ```\d```
```
[\da-z\.-]
```
This expression will accept any single digit character or any lowercase letter from ```a-z``` and a dot ```.``` or dash ```-```.

- The alphanumeric character class ```\w```
```
[\/\w \.-]
```
This expression will accept the forward slash character ```/```, any word character, a space, and a dot ```.``` or dash ```-```.

It is important to note that while ```.``` denotes a character class to match for wildcard characters, the ```\.``` seen in the expressions above is looking for the dot character  ```.``` explicitly, and not referencing the character class represented by the same dot ```.``` character. 

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
  This grouping contains two ```?``` quantifiers. This expression is looking for an ```http://``` or an ```https://```. A *single* ```s``` is optional. The same is true for the entire expression included in the parentheses, which explains why the grouping is followed by a ```?```. Therefore, a valid URL may begin with ```http://``` or ```https://```, or it may not begin with either of them at all (the input might begin with ```www.```).
  
 - The domain name ```(google or wikipedia)```: 
 ```
 ([\da-z\.-]+)\.
 ```
 This grouping contains the ```+``` quantifier. The bracket expression will accept any single digit character, any lowercase letter from ```a-z```, and the special character dot ```.``` or dash ```-```. The ```+``` quantifier indicates that the pattern must match 1 or more times. 
 
 - The top-level domain ```(.com, .org, .etc)```: 
 ```
 ([a-z\.]{2,6})
 ```
 This grouping contains the ``` { 2, 6}``` quantifier. This is used to signify that the pattern must match a minimum of 2 and a maximum of 6 times. Specifically, the bracket expression indicates that any lowercase letter ```a-z``` and a dot ```.``` will produce a match. 
 
 - The file path or endpoint ```(/home, /about, /etc)``` :
 ```
 ([\/\w \.-]*)*
 ```
 This expression signifies that the expression ```[\/\w \.-]``` may match 0 or more times and that ```([a-z\.]{2,6})([\/\w \.-]*)``` may also match 0 or more times. In the former case, a forward slash ```/```, any word character (equivalent to querying ```[a-zA-Z0-9_]```, a space, and a dot ```.``` or dash ```-``` will produce a match. Alternatively in the latter case, a file or endpoint may not match at all (the URL can be a plain domain). 

### Grouping and Capturing
While our "Matching a URL" regex is fairly straightforward, regular expresions can quickly grow more complicated in an effort to check multiple parts of a string to determine that different sections fulfill different requirements. To break these sections up and **capture** certain patterns, we can use **grouping** constructs. 

The primary way of capturing a certain pattern is by surrounding the expression we wish to capture in parentheses like this: ```(...)```. Grouping constructs are powerful because they allow us to concatenate patterns or append a quantifier to a group instead of a singular character.

We use the group capturing construct four times in our URL expression:
- ```(https?:\/\/)```: Capture the protocol of the URL.
- ```([\da-z\.-]+)```: Capture the domain of the URL.
- ``` ([a-z\.]{2,6})```: Capture the top-level domain of the URL.
- ```([\/w \.-]*)```: Capture any file paths or endpoints. 

### Bracket Expressions

A bracket expression is a range of characters inside a set of square brackets ```[...]``` that represents a pattern we want to match within an input string. **Bracket expressions** are known as a **positive character group** because they outline the characters we want to include. For example, ```[abc]``` will look for a string that includes ```a``` or ```b``` or ```c```, regardless of the length of the string. Therefore, the following examples would match: ```"aaa"```, ```"bin"```, ```"court"```, ```"abracadabra"```, and ```"bca"```. 

You'll commonly see a hyphen ```-``` used between alphanumeric chracaters (letters and numbers only) to represent a range of those possible characters. This means that ```[a-c]``` and ```[abc]``` will look for the same pattern. 

In our "Matching a URL" regex example, we can break down the bracket expressions as follows:

- ```[\da-z\.-]``` will accept any digit, a lowercase letter from ```a-z``` and a dot ```.``` or dash ```-```.
- ```[a-z\.]``` will accept any lowercase letter from ```a-z``` and a dot ```.```.
- ```[\/\w \.-]``` will accept a forward slash ```/```, a word character, a space, a dot ```.```, or dash ```-```.

### Greedy and Lazy Match

Quantifiers can be purposed to look for a **greedy** or **lazy** match. A greedy match implies that the quantifier will force the search of an input string to match as many occurrences of particular patterns as possible, while a lazy match denotes that a quanitfier will force the search of an input string to match an occurrence of particular patterns as little as possible. 

- The ```*```, ```+```, and ```{}``` quantifiers are all ways of specifying greedy matches since they force the search to carry through until the end of the string (with the exception of the ```{}``` if a second parameter were to be passed in).
- The ```?``` quantifier would only match the specifed pattern before this character one or zero times, implying that it might not reach the end of the input string when searching for a match. 

We see examples of the two types of matches below in our "Matching a URL" regex below:

 - The domain name ```(google or wikipedia, for example)```: 
 ```
 ([\da-z\.-]+)\.
 ```
 The ```+``` quantifier indicates that the pattern must match 1 or more times. 
 
 - The top-level domain ```(.com, .org, .etc)```: 
 ```
 ([a-z\.]{2,6})
 ```
 This grouping contains the ``` { 2, 6}``` quantifier. This is used to signify that the pattern must match a minimum of 2 and a maximum of 6 times.
 
 - The file path or endpoint ```(/home, /about, /etc)``` :
 ```
 ([\/\w \.-]*)*
 ```
 This expression signifies that the expression ```[\/\w \.-]``` may match 0 or more times and that ```([a-z\.]{2,6})([\/\w \.-]*)``` may also match 0 or more times.  This implies that a file path or endpoint may not match at all (the URL can be a plain domain). 

## Author

Christian Flores is a student of the Coding Bootcamp associated with the University of California, Berkeley. To see more of his work visit his [GitHub Profile](https://github.com/c1flores)
