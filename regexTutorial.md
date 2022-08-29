# Regex Tutorial: Email validator

We will break down a specific regex that searches pattern of an email address. 

## Summary

Regular expressions, regex in short, are patterns that match specific combinations in a string. In this tutorial, we will go over a regular expression that searches for pattersn found in an email address. This regex can be sued to validate if a user inputed a valid email address. The regex we will break down is as follows: 

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

To summarize, the requirements this regex defines are
- The username (the string before the @) is only comprised of lowercase letters between a-z, numbers between 0-9, an underscore, period or a dash.
- The username can be of any length more than 1.
- The mail server domain is only comprised of lowercase letters between a-z, numbers between 0-9, a period or a dash.
- The mail server domain can be of any length more than 1.
- The top level domain is only comprised of lowercase letters between a-z or a period.
- The length of the top level domain must be between 2-6 of the above characters

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Bracket Expressions](#bracket-expressions)
- [Grouping Constructs](#grouping-constructs)
- [Character Classes](#character-classes)
- [Character Escapes](#character-escapes)
- [Resources](#resources)

## Regex Components

### Anchors

Anchors match a position before or after characters: 

- ` ^ ` - The caret anchor matches the beginning of the text
- ` $ ` - The dollar anchor matches the end of the text

The beginning and end of the matching email regex include anchors which means must start with the requirements `[a-z0-9_\.-]` and end with `[a-z\.]`

### Quantifiers

Quantifiers match a number of instance of a character, group, or character class in a string:

- ```{n}``` where n is the desired number of characters to match
- ```{n,m}``` provides a range of the desired number of characters to match

For example: 

```
let str = 'Quantifiers are pretty cool';
let re = /o{2}/;
console.log(str.match(re)); // ["oo"]
```

```
let str = 'Quantifiers are pretty cool and gooood';
let re = /o{3,5}/;
console.log(str.match(re)); // ["oooo"]
```

There are shorthands for commonly used ranges as shown in table below: 
| Quantifier | Same As | Description |
|------------|---------|-------------|
| *          | {0, }   | Match zero or more times |
| +          | {1, }   | Match one or more times  |
| ?          | {0,1}   | Mathc zero or one time   |

In the case of the email regex, we see that the bracket expression for username and mail server domain end with a `+`. This means that the bracket expression can match one or more times, therefore they can be of any length more than 1. The top level domain ends with `{2,6}` which means that it can only be between 2-6 characters long. 

### Bracket Expressions

Bracket expressions represent a range of characters we want to match. The expression within the brackets can be a range of literal or meta characters. 

For example: 

```
let str = 'I bought this car for only $1500';
let re = /[0-9]+/; // the same as \d
console.log(str.match(re)); 
// output ['1500']
```

In the case of the email regex, there are three bracket expressions: one in the username, one in the mail server domain, and one in the top level domain. The range the username, `[a-z0-9_\.-]`, is defined by lowercase letters (`a-z`), numbers (`0-9`), and special characters (` _ `, ` . `, ` ' `). 

### Grouping Constructs

Grouping constructs allows regex to match multiple parts of a string to check different requirements at different sections. In order to group sections, we use parenthesis `()` and the expressions within each parenthesis are subexpressions. 

For example:

```
let str1 = '123.abc';
let str2 = '123.123';
console.log(/(\d+).([a-z]+)/.test(str1)); // output: true
console.log(/(\d+).([a-z]+)/.test(str2)); // output: false
```

In the case of the email regex, the requirements for username, mail server domain, and top level domain are separated between `()`. 

### Character Classes

A character class helps distinguish differnt kinds of characters. The table below shows common character classes. 

| Character | Description | Same As | 
|-----------|-------------|---------|
| ^ | Within brackets, matches anything that is not enclosed in the brackets. If outside brackets, treat as anchor |
| . | Matches any character expet a newline character `\n`|
| \d | Matches any Arabic numeral digit | `[0-9]` |
| \D | Matches any characters that is not a digit | `[^0-9]` |
| \w | Matches any alphanumeric character from the Latin alphabet | `[A-Za-z0-9]` |
| \W | Matches any character that is not from the Latin alphabet | `[^A-Za-z0-9_]` |
| \s | Matches a single white space character (includes space, tabs and Unicode spaces) | `[ \f\n\r\t\v\u00a0\u1680\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]` |
| \S | Mathces a single character other than white space | `[^\f\n\r\t\v\u00a0\u1680\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]` |
| \ | Indicates the following character should be treated specially or to be 'escaped' |

In the case of the email regex, `\d` was used in the mail server domain to match digits. This can also be replaced with `[0-9]` and would function the same. Alternatively, the username can be replaced to `[\da-z_\.-]+` and would also function the same. 

### Character Escapes

Character escapes are useful to expand the vocabulary of a regex. The use of backslash `\` denotes that the following character should be treated specially or to be escaped. If the character following the `\` are already used as a character class or a special character, then it becomes the literal character. The example below shows matching the slashes in the date. Without the backslash before the slashes, we get an invalid error since it closes the regex. 

For example:

```
let str = 'Today is 06/12/2022'
console.log(/\d+/\d+/\d+/.test(str)); // output: invalid expression flags 
console.log(/\d+\/\d+\/\d+/.test(str)); // output: true
```

In the case of the email regex, we use `\.` to denote we are looking for a the literal period. 

## Resources 

- [MDN Web Docs- Regular Expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
- [Javascript Tutorial](https://www.javascripttutorial.net/javascript-regex/)

## Author

- [Adriane Ocampo- Portfolio](https://ocampoad.github.io/Adriane_Ocampo_Portfolio/)
- [Adriane Ocampo- Github](https://github.com/ocampoad)