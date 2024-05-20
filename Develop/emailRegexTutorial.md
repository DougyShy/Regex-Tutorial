# Email Regex Tutorial - Email Address Format Verification

For this tutorial I will be using a regex to check a string for email accuracy and security purposes.  
A regular expression might look quite cryptic but it can be worth its weight in gold.   
With a (semi) simple test this regex can determine if a string is a properly formated email address.  
You can even tweak it to your specific standards to only allow certain characters or internet domains.  

## Summary

You typically see this regex used on login and sign in pages as well as in password/account recovery.  
The regex code in Javascript would be as follows:

// Declare a regular expression to 'test' any email string attempt
sconst regexTestEmail = /^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/


// Create an email to test  
const testEmail = 'doug_scheible@yahoo.com';  

// Test email string - EXAMPLES
console.log(regexTestEmail.test(testEmail))   // True  
console.log(regexTestEmail.test(cantUse!inUserName@yahoo.com))   // False  
console.log(regexTestEmail.test(working-email@not%workingAddre$$Here.com))   // False  
console.log(regexTestEmail.test(working-email@working-address.morethan6))   // False  

Note: Most people understand the standards of emails but email fields can easily be messed up or mistaken by the user
and even sometimes used maliciously by hackers so it's important to make sure what characters and expressions are allowed to be
passed to the backend.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

    Since this regex is accepting a string and we are comparing an entire string our anchor '^' will start at the beginning
    To mark the start of the string anchor '/^....    
    To mark the end of the string anchor: '....$/' 

### Quantifiers

    In this email regex example we are using two quantifiers. Quantifiers define the quantity or repetition of the preceding character or group. 
    They allow you to specify how many times a particular element should occur. If an element is not in the quantified character class

    The first quantifier used is the plus (+). In our case, using the + ensures that there is at least one or all components
    of the Character Class (see table of contents) in the username part of the email.

    '[a-zA-Z0-9._%-]+'   // this is equivalent to '[character class definition]+'

    The second quantifier used is also the plus (+). In our case, using the '+' ensures that there is at least one or all components of the 
    Character Class (see table of contents) in the address part of the email.

    [a-zA-Z0-9.-]+

    Note: See Character Classes and Bracket Expressions (table of content) for specific explanations about what comes before the 
          quantifier in the brackets.

### OR Operator

    The OR operator '|' is not used in this email regex tutorial.

### Character Classes

    As mentioned above in Quantifiers (see table of contents), Character Classes will be definiing what characters are allowed on each 
    portion of the email string. This helps to validate any emails that come through and make sure that the email format is up to 
    your specifications.

    In this particular regex we have 3 Character Classes:

    We can break the first Character Class down as follows:
        a-z : all lowercase letters
        A-Z : all uppercase letters
        0-9 : any numbers
    
        This next section really just includes specific characters that are allowed to be used:
        Individual characters '.', '_', '%', and '-' may be used in the username portion of the email string.

    As you can see, the second Character Class is very similar to the first:

        The only difference is that individual characters '_' and '%' may not be used in the address portion of the email string.

    Finally, the third Character Class is pretty basic:

        Only characters from a/A to z/Z '[a-zA-Z]' may be used in the domain portion of the email string. 

### Flags

    In a regular expression, flags are optional parameters that modify the behavior of the pattern matching. I do not believe 
    this regex uses any flags.

### Grouping and Capturing

    Although my example is only grouped into one single expression, it could easily be divided into three so that captured 
    values can be accessed seperately. Instead of the original example you could break this down into three groups for capturing. 

    Original regex : /^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/
                       (----------------------------------------------)

    Grouped regex: /^([a-zA-Z0-9._%-]+)@([a-zA-Z0-9.-]+)\.([a-zA-Z]{2,6})*$/
                     (----------------) (--------------)  (-------------)          

### Bracket Expressions

    Bracket Expressions are very similar to Character Classes. The Bracket Expressions operator ([]) is used to define a character 
    set or a range of characters that can match a specific position in the email address.

    This regex has three bracket expressions each with similar characteristics but also each unique: 

        /^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/
           [-------------]  [-----------]   [------]

        An explanation of what is inside of of each bracket can be found in the Character Class section (see table of contents)

### Greedy and Lazy Match

    In this particular email regex we have a Greedy Match. Our greedy match comes at the end when we want to test our domain. 
    We have established that the domain name will have a filtered value of only lowercase and uppercase letters. 
    But how many? In this case, placing our greedy match directly after our bracket expression we can make sure that the 
    domain is at least 2 characters and no more than 6. 

    /^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/
                                                {---}

    Note: In order to validate at least two characters: {2,}
          In order to validate no more than six characters: {,6}                                                

### Boundaries

    The boundaries in this regex example are basically our Anchors (see table of Contents). Our first boundary is our first 
    anchor '^' right before the opening '/' and starting at the begging of the user address. In order to let the computer know 
    that the string boundary has been reached the '$' is used at the end of the expression right before the closing '/'.

### Back-references

    In a regular expression, a back-reference allows you to match the same text that was matched by a capturing group earlier in 
    the pattern. This is useful when you want to ensure that a part of the string repeats exactly as it did before. However, in 
    the context of validating email addresses, back-references are not typically necessary

### Look-ahead and Look-behind

    In the context of a regular expression (regex), look-ahead and look-behind are zero-width assertions that allow you to check 
    if a certain pattern is followed or preceded by another pattern without including the matching content in the final match. 
    These assertions are useful in constructing more complex and precise regex patterns. I don't believe that there is a need for 
    this component in this email regex as it is already pretty well positively filtered.

## Author

(5.20.24)

My name is Doug Scheible. Currently I am attending a UTSA Fullstack Development Bootcamp. I enjoy web development and problem solving. I am a beginner/amatuer coder who has entry level experience mostly in Javascrip, SQL, and Python
Gist: https://gist.github.com/DougyShy/74fbcab699bfebf8ce688c10beba14db
Github: https://github.com/DougyShy
Email: doug_scheible@yahoo.com
Fell free to text me @ 123.456.7890
