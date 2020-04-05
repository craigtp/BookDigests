# Book Digest: The Art Of Readable Code

Title     : The Art Of Readable Code  
Author(s) : Dustin Boswell, Trevor Foucher  
ISBN-10   : 0596802293  
ISBN-13   : 978-0596802295

## Chapter 1 - Code Should Be Easy To Understand
- All code should be easy to understand.
- Code should adhere to "The Fundamental Theorem of Readability" which is that code should be written to minimize the time it would take for someone else to understand it.
- Minimizing lines of code can help understanding, but even better is minimizing the time-until-understanding.
- It can appear that other constraints such as well-structured, well-architected code or easy-to-test code might sometimes conflict with making the code easier to understand, but these other goals don't interfere too much at all.  Making your code easy to understand often leads to code that is well architected and easy to test anyway.

## Chapter 2 - Packing Information Into Names
- Pack lots of information into names.
- It's better to be clear and precise that to be cute with names.
- Using names like `tmp` for a variable should only be used in cases when being short-lived and temporary is the most important fact about that variable.
- Instead of using names like `i`, `j`, `k` for iterators/indexes, prefix them with the word or letter of the array into which they index - i.e. `clubs[ci].members[mi]`
- When naming a variable, function, or other element, describe it concretely rather than abstractly.
- A variable's name is like a tiny comment.
- If you variable is a measurement, such as an amount of time or a number of bytes, it's helpful to encode the units into the variable's name.
- Many security exploits come from not realizing that some data your program receives is not yet in a safe state. For this, you might want to use variable names like `untrustedUrl` or `unsafeMessageBody`. After calling functions that cleanse the unsafe input, the resulting variables might be `trustedUrl` or `safeMessageBody`.
- Shorter names are ok when used for shorter scope.  For names with larger scope, longer and more descriptive names should be used.  The name needs to carry enough information to make it clear.
- Project-specific abbreviations are usually a bad idea as they can appear cryptic and intimidating to those new to the project.  The golden rule is would a new teammate understand what it means? If so, then it's probably ok.
- The way you use underscores, dashes, and capitalization can also pack more information in a name.
- Depending on the context of your project or language, there may be other formatting conventions you can use to make names contain more information. Following conventions for languages, platforms or frameworks can help give meaning to names.  For example, in the jQuery library, whose function name is a `$`, you could prefix jQuery result variables with a `$` symbol too to make it clear that the variable is a jQuery result.

## Chapter 3 - Names That Can't Be Misconstrued
