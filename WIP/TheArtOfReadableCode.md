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
- Actively scrutinize your names and ask yourself, "What other meanings could someone interpret from this name?"
- Don't use words like `filter` since they're ambiguous.  For example, code such as `myObjects.Filter(year > 2010)` isn't clear as to whether the method result includes objects with year greater than 2010 or excludes them.  Include or Exclude would be a better name here.
- The clearest way to name limits of values is to prefix them with either `min_` or `max_`.
- When dealing with names that represent inclusive ranges, prefer to use words such as `first` and `last` as these names imply inclusion.
- When dealing with names that represent either inclusive or exclusive ranges, prefer to use words such as `begin` and `end`.
- When naming booleans, adding words such as `is`, `has`, `can` or `should` to the beginning of the name can make the name much clearer.  For example, a function named `SpaceLeft()` sounds like it might return a number, whereas `HasSpaceLeft()` sounds much more like a true/false value.
- Avoid using negated terms in boolean values as these cause confusion.  For example, don't use `disable_ssl` but use something like `use_ssl`.
- Always attempt to match your names to the expectations of users.  For example, many programmers understand a function prefixed with `get` to refer to a simple, non-compute intensive property accessor or similar, so make sure that you don't have a function prefixed with `get` that performs intensive computation.

## Chapter 4 - Aesthetics
- A lot of thought goes into the layout of things like magazine articles.  Good source code should be just as "easy on the eyes".  Use a consistent layout and make similar code look similar.
- Rearrange line breaks for similar/repeated code so that each has the same layout.  Use column/horizontal alignment to help achieve this.
- When code is repeated but can wrap differently for each invocation (such as in unit tests), wrap the code in methods to clean up the irregular layout.
- Pick a meaningful order to code.  If you have to declare five different variables and then use them in checks, ensure the checks are in the same order as the declaration.
- When defining a large list of methods (e.g. inside an interface), break those methods into logical groups and perhaps add a single-line comment above each group to help clarify.
- Break method code into "paragraphs".  If you're reading some data, processing, then writing it out, group the lines for each of those sections into their own "paragraph" perhaps with a single-line comment to help clarify the intent.
- Consistent style is more important than the "right" style.  e.g. Method braces can be either K&R style or Allman style.  Neither is "right" or "wrong", but make sure to follow the same convention used throughout the entire codebase.

# Chapter 5 - Knowing What To Comment
- 