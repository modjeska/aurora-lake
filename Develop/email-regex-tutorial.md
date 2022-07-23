# Understanding Regular Expressions
Many of us have used a search functionality in the past, whether it's through a text editor, word document, or even through the browser you are using to view this right now. Most commonly known as word finders, these search functionalties allow us to search for a specific word, number, or phrase inside a text area. Although the use of these word finders can be extremely helpful, you are limited in the ability to search for a group or pattern of words that are similar in nature, but not written exactly the same in terms of characters. This is where regular expressions shine, through the combination of coded characters, regular expressions (or REGEX for short) allow us to search for specific patters inside a text area. But let me dive deeper below.

## A Deeper Dive Into REGEX
/assets/images/regex-example.png
Today we will be refering to email addresses as the pattern we are searching for. The above image displays a convoluded jarble of characters that look as if someone smacked their keyboard to make. And although they do look complex and hard to understand, the syntax for these coded characters is quite simple.  We can better understand this snippet of characters by defining what each one means. We will first be taking a look at literal characters, which are the key part in finding specific characters.

## Table of Contents
- [Literal Characters](#literal-characters)
- [Meta Characters](#meta-characters)
- [Quantifiers](#quantifiers)
- [Positioners](#positioners)
- [Character Classes](#character-classes)
- [Breaking It Down](#breaking-it-down)
- [Where To Use REGEX](#where-to-use-regex)
- [Author](#author)

## Regex Components
In this gist, we will be breaking down this regular expression
```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ ```
and understanding how it can look like an email
```example@gmail.com ```

### Literal Characters
The good thing about literal characters is that they are short and sweet. They are simply characters entered into a regular expression that **LITERALLY** mean what they are. So an example of this would be the letter a or z, or the number 0 or 9, like provided in the regex photo above. Literal characters will be used to find words or patterns containing these characters, but there is more to the story, enter.... **META CHARACTERS**.

### Meta Characters
This is where things start to get exciting, meta characters are characters mixed with special characters to mean something more than they are. Example of some meta characters include:
- \d = this character refers to any digit from 0-9
- \w = refers to any letter a-z (regardless of capitalization) and digits 0-9
- \s = refers to any white space (empty space between words/digits/characters)
- \W = refers to the opposite of \w (anything that is not a letter or digit)
- \S = refers to the opposite of \s (anything other than white space)
- .(period) = refers to **any character**
- *(astrix) = refers to 
- \. = this just refers to a **literal** period
- \( = this just refers to a **literal** opening parenthesis symbol

Now with this information we can already start to break down our example regex, but lets dive even DEEPER.
 
### Quantifiers
Quantifiers allow us to search for **any** number of a given set of characters. Remember that these quantifiers are ended after a space or special character. Here is a list:
- *(astrix) = refer to 0 or more
- +(plus) = refer to 1 or more
- ? = refer to 0 or 1
- {min, max} = set a minimum and maximum search parameter
- {n} = n is the value which represents how many searches for a character

So let's take what we have learned so far and try it:
- ```a{3}```
  - This would be searching for any word with the **literal** character a 3 times in a row
- ```\w+```
  - This would be searching for any word with at least one or more characters and digits 

### Positioners
With positioners we can establish an area within a regex that contains certain boundries:
- ^ = the caret symbol refers to the start of a line
- $ = refers to the end of a line
- \b = is a word boundry
- / / = a patterned group you are searching for
- () = a subexpression

So in the provided regex example ```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ ``` we can see that the whole expression is a patterned group we are searching for (emails). We can then see the caret symbol indicated the start of a line and the line ends at the $ symbol. We use these because we could have another line containing different parameters inside our patterned group. We can then see subexpressions indicated by the () symbols, to seperate these character classes from others, which we will talk about next.

### Character Classes
This is where everything comes together, **character classes**. These classes give us a way to search for multiple different characters regardless if isn't found. Think of it as an **OR** statement. For example, we want to look for a literal character a **OR** a 9, this would look like ```[a9]```. Here is a list of character classes we can use:
- [ ] = will search for any character entered, and return what is found
- [a-z] = the "-" symbol when **not** the first character inside brackets will refer to the range of characters provided, regardless of capitalization
- [^a-g] = the "^" symbol when **not** the first character inside brackets will refer to anything that is not the letters a through g, regardless of capitalization

Using everything we have learned in this gist, we can take a look at this regular expression and try to break it down, piece by piece.

### Breaking It Down
```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ ```
So, from left to right, lets break down what we are looking at
- We start with the / symbol to indicate this is a patterned group.
- The ^ symbol indicates the start of a line.
- () symbol indicates the beginning and end of a subexpression.
  - We have 3 subexpressions in this regex from ^ to $.
- Inside the subexpression we have [] brackets indicating the start of a character class.
  - We have 3 character classes in this regex.
- Inside our brackets we are searching for any character a through z (regardless of caps).
  - We are also looking for any digit from 0-9.
- We are then looking for a **literal** underscore symbol "_".
- Then we are looking for a **literal** period, refer to the metacharacter section if lost.
- And to end our character class we are looking for a slash "-" symbol.
- So that completes are character class "[]". The reason for the brackets is to indicate that we are looking for any of these parameters, so if there are no numbers for example, they will be excluded and a set of letters a-z will be returned instead.
- Following the end of our [] brackets we see a plus symbol indicating we are searching for at least one result from our character class. (empty characters not allowed).
- We then have a **literal** @ symbol as follows the traditional email syntax.
- We then have another subexpression that follows the previous, it contains:
  - A character class
  - \d any digits 0-9
  - any letter a-z or A-Z
  - a **literal** period
  - and a slash symbol
- A plus symbol to indicate at least one result from this character class (no empty fields).
- We then have a literal perion to continue our email syntax.
  - We are currently at this stage in the regex:
    - some.letters.or903@somecharacters.
- To finish off our expression, we have another subexpression indicating:
  - Any letter a-z/A-Z
  - A period
- We then have a quantifier which is contained in our final subexpression, indicating that we are searching for a minimum of 2 or a maximum of 6 characters from this result.
  - This can refer to the end of an email's syntax.
    - Ex: .com/.net/.org/.edu
- We then finish out the expression with the $ symbol to indicate the end of our line.
- And finally a / symbol to indicate the end of our pattern.

Pretty easy right? Give yourself a pat on the back for reading this far, you now know how to search for a email using **regular expressions**!

### Where To Use REGEX
Now that you know how to read REGEX, where can you use it? Many progamming languages support the usage of regular expressions through standard libraries.

## Author
Hi! This is Dante, the creator of this gitHub gist, I am currently a student enrolled in the UCI coding bootcamp. Learning some code over the summer has been a blast and I am very excited to see where it takes me. Thanks for reading!

You check out my github profile [here](https://github.com/modjeska). 
