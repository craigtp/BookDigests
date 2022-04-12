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
- Be careful with naming things using words that are both nouns and verbs.  Words like `Count()`, `Record()` etc can used as both a noun and a verb and so methods named as such can be confusing to the reader as you exactly what the method does.
- Always attempt to match your names to the expectations of users.  For example, many programmers understand a function prefixed with `get` to refer to a simple, non-compute intensive property accessor or similar, so make sure that you don't have a function prefixed with `get` that performs intensive computation.

## Chapter 4 - Aesthetics
- A lot of thought goes into the layout of things like magazine articles.  Good source code should be just as "easy on the eyes".  Use a consistent layout and make similar code look similar.
- Rearrange line breaks for similar/repeated code so that each has the same layout.  Use column/horizontal alignment to help achieve this.
- When code is repeated but can wrap differently for each invocation (such as in unit tests), wrap the code in methods to clean up the irregular layout.
- Pick a meaningful order to code.  If you have to declare five different variables and then use them in checks, ensure the checks are in the same order as the declaration.
- When defining a large list of methods (e.g. inside an interface), break those methods into logical groups and perhaps add a single-line comment above each group to help clarify.
- Break method code into "paragraphs".  If you're reading some data, processing, then writing it out, group the lines for each of those sections into their own "paragraph" perhaps with a single-line comment to help clarify the intent.
- Consistent style is more important than the "right" style.  e.g. Method braces can be either K&R style or Allman style.  Neither is "right" or "wrong", but make sure to follow the same convention used throughout the entire codebase.

## Chapter 5 - Knowing What To Comment
- The purpose of commenting is to help the reader know as much as the writer did.
- Don't comment on facts that can be derived quickly from the code itself.  Quickly is important here, it's ok to add a comment that may not present any new information but is easier and quicker to read and understand than the code it is commenting.
- Comments shouldn't make up for bad names.  If a variable or function's name isn't clear such that you feel it needs a comment, fix the name instead.  A good name is better than a good comment.
- A lot of good comments can come out of recording the important thoughts you had whilst writing the code.
- Use comments that teach the reader something about the code.  A comment stating, for example, that you're using a binary tree instead of a hash table as tests showed the binary tree to be 40% faster give great insight and prevent would-be code optimizers from wasting their time.
- Use comments that help explain issues with the code, too.  A comment indicating that a class is getting too large along with some ideas of how to improve it, can help readers to get started on refactoring.  This extends to specific flaws or work-arounds that are present in the code such as using a better algorithm, dealing with more use cases etc.  These will most often take the for of `TODO:` style comments.
- Add comments to your constants.  Even with a good name, e.g. `NUM_THREADS`, it's helpful to add a comment to indicate the general use of the constant and what realistic values might be assigned to it - e.g. `// Threads should be multiple of the available core in the machine`.
- If your chosen language has specific "hacks" to perform some function that are non-intuitive to the reader, make sure to comment these.  If an API has a `.Clear()` method but you use another mechanism to empty the object (perhaps to ensure that memory is reclaimed where it might not otherwise be), ensure this is explicitly called out in a comment.
- Comment likely pitfalls in the code. If code could be seen as surprising or could be misused, call it out. For example, if you have a method that sends an email and that method makes calls to external libraries that can take some time to complete, ensure the comment on the method indicates this fact.
- Include high-level, "big picture" comments that document the general execution flow of the code.  These comments are the same as verbal comments you might make if you were giving a new team member a tour of the code base. e.g "This is the glue code between the business logic and the database and none of the application code should call this directly."
- Use Summary comments to describe chunks of code in longer functions.  e.g. If you're performing a few nested loops, you could comment above to say "Find all items that customers purchases for themselves". Such comments also act as a bullet point summary list of what the function does.
- Some prevailing wisdom says to only comment the "why" of the code, not the "what" or the "how", but this can be too simplistic and open to interpretation.  It is better to simply comment when it will help a reader to understand the code more easily.

## Chapter 6 - Making Comments Precise And Compact
- Comments should have a high information-to-space ratio.
- Avoid ambiguous pronouns such as "it", "this" etc.  Be explicit with what you're referring to, especially when a pronoun could be interpreted to mean different things.
- Keep sentences short and too the point.  Instead of saying "Depending on whether we've already crawled this URL before, give it a different priority", instead say "Give higher priority to URLs we've never crawled before".
- Always describe function behaviour precisely.  If you comment a function that counts the number of lines in a file, the definition of a "line" isn't completely clear (does an empty line count?).  Better to describe the function to say that you count the number of newline bytes in a file.  Use example input/output values to help.
- Always state your intent in comments.  Instead of using a comment that simply describes the code e.g. "Iterate through the list in reverse-order", use a comment that describes the intent behind the iteration e.g. "Display each price, from highest to lowest".  A positive side-effect of such comments are that they can potentially highlight bugs in the code, effectively acting as a redundancy check.
- If your language doesn't allow named arguments for method parameters, use comments in front of calls to the method to help clarify what the values represent. e.g. Instead of code such as `Connect(10, false)`, write this `Connect( /* timeout_ms */ 10, /* use_encryption */ false)`
- Keep comments brief by using words that pack a lot of meaning and will be well understood by readers.  e.g. You can simply use the phrase "caching layer" rather than having to describe exactly what one is.

## Chapter 7 - Making Control Flow Easy To Read
- Make all conditionals, loops and other changes to control flow as natural as possible.  They should be written in a way that doesn't cause the reader to stop and have to re-read the code.
- When comparing values in a conditional, ensure the left-hand side is the expression being "interrogated" and the right-hand side is the expression being compared against, which should be more consistent. i.e. `if (length > 10)` rather than `if (10 < length)` or `if (bytes_received < bytes_expected)` rather than `if (bytes_expected > bytes_received)`
- When writing if/else statements, prefer to deal with either the positive use case inside the first if.  Alternatively, if the negative use case is either simpler or more interesting, deal with that inside the first if, leaving the more complex or negative cases to the else block.
- Be careful with the ternary operator.  It should only be used to switch between simple expressions that don't require further computation. i.e. `time_str += (hour >= 12) ? "pm" : "am"` is fine, but `exponent >= 0 ? mantissa * (1 << exponent) : mantissa / (1 << -exponent)` is far more difficult to read.
- Instead of minimizing the number of lines, a better metric is to minimize the time needed for someone to understand the code.
- Avoid do/while loops.  They place the condition below the code that they're evaluating which is the opposite of for, if & while.  This often forces the reader to read the code twice.  All do/while loops can be re-written to use another for of loop.
- It's perfectly fine to have multiple places in which to return early from a function.  This is most often seen with guard clauses near the top of the function.
- Try to avoid the `goto` statement.  Some goto's, say a single goto at the bottom of a function that performs some clean-up can be fine, however, multiple goto targets and especially goto's that go upwards are problematic and lead to spaghetti code.
- Minimize nesting of conditionals.  One way to achieve this is to handle failure cases and return early from the function.  If you have nesting inside of a loop, consider replacing the nesting with a `continue` statement.
- Think about the "flow" of your program from a high-level.  Your code should ideally be easy to read and follow from top to bottom, like prose.  Try to minimize the areas of code that require conditionals or loops to avoid the reader from having to mentally "jump around" the code as they're reading it.

## Chapter 8 - Breaking Down Giant Expressions
- Large chunks of code should be broken down into smaller, more digestible pieces.  Recent research indicates that most of us can only hold 3 or 4 "things" in our head at one time, so understanding large blocks of code is difficult.
- Introduce an "explaining" variable.  This is a variable that holds a smaller sub-expression, is appropriately named and then used in the larger expression to give more meaning.  e.g. `var userName = line.split(':')[0].strip()` then `if userName == "admin"` rather than `if line.split(':')[0].strip() == "admin"`
- Introduce "summary" variables to hold expressions that are reused.  e.g. instead of doing `if(request.user.id == document.user_id)` multiple times, introduce a variable `var userOwnsDocument = (request.user.id == document.user_id)` and use the variable inside the conditionals instead.
- Use De Morgan's Laws to simplify boolean logic.  Instead of writing `if (!(file_exists && !is_protected))` we can simplify this to `if (!file_exists || is_protected)`
- Don't abuse short-circuiting evaluation of boolean operators in order to perform "clever" logic.  Break the logic down into multiple lines and use explaining variables to make it easier to understand.
- When implementing complicated logic, it's often the case that you'll need a creative approach in order to simplify the problem. e.g. Checking if time ranges overlap with each other can lead to multiple boolean comparisons, however, checking if time ranges _don't_ overlap is simpler and achieves the same goal by looking at the problem from an opposite/alternative perspective.
- Using explaining or summary variables can help to simplify large blocks of code comprised of individual expressions.  Each expression may not be too complex, but when placed all together, the "block" of code can become difficult to read so use such variables to both reduce duplication and improve readability.

## Chapter 9 - Variables And Readability
- Remove unnecessary variables.  If a variable holds a simple expression that is easily understood, use the expression directly instead of assigning to a variable. i.e. `var date = DateTime.Now` is redundant.
- Beware of using variables to hold an intermediate result, usually when searching some collection within a loop.  It's often better to handle whatever behaviour is required on the found element immediately rather than assigning to a temporary variable to be handled later, outside of the loop.
- Beware of using "control flow" variables, which are used only to steer the flow of execution through the program and don't contain any real data (often used as a conditional check inside a `while` statement etc.)  Such variables can almost always be replaced with a better control flow structure.
- Keep the scope of variables as small as possible.  Your variable should be "visible" to as few lines of code as possible.  This effectively reduces the number of variables a read has to think about at any one time.
- Don't declare all variables used in a function at the top of the function.  If a variable is not used until much further down in the code, declare the variable close to it's actual usage.
- Prefer write-once variables.  The more places in which a variable's value can change, the harder it is to reason about its current value.

## Chapter 10 - Extracting Unrelated Subproblems
- Aggressively identify and extract unrelated subproblems in code.  Look at a function's high-level goal and examine each line of code.  Lines that do not work _directly_ to the goal should be extracted into separate functions.
- Create lots of general purpose code.  General purpose code is great because it's completely decoupled from the rest of your project and domain.  Such code is easier to develop, easier to test and easier to understand.
- Create functions that hide details of interfaces that are unintuitive. e.g. Deleting a cookie value for a website requires setting the expiry date to a date in the past.  We can wrap this functionality so that calling code simply needs to call a function named `delete_cookie`, which is more intuitive.
- Create functions that wrap the "glue" code that often required within other functions.  e.g. Encrypting a string and returning an ASCII-armoured string result will require lots of conversions to and from byte arrays, this can be extracted to helper functions.
- Whilst unrelated subproblem code should be aggressively extracted, it's possible to go too far.  Each new added function has a cost in readability so be sure to balance that when refactoring.
- The key goal when refactoring unrelated subproblems is to separate the generic code from the project-specific code.

## Chapter 11 - One Task At A Time
- Code should be organised so that it's doing only one task at a time.  Breaking code into separate functions is good, but even within the same function, code should be logically grouped for each task.
- Tasks can be small.  For example, code that reacts to a user clicking a button to up vote or down vote something is actually performing two tasks - one to interpret the button click and parse it into numerical values and one to update the overall score.
- Try to identify all of the tasks that a piece of code is doing.  There's often multiple tasks at play - iterating a list, comparing values, computing results etc.  If each task isn't able to be easily extracted into its own function, try to group the tasks within the same function.  Using "summary variables" can help here.

## Chapter 12 - Turning Thoughts Into Code
- Your code should be written following the key words you'd use to describe its function to a colleague in plain English.  First, describe the code in plain English, look for the key words and phrases and write your code to match this description.
- Using this technique, we can create code that is very readable. For example, if we have a function to determine if the user is authorised to access some resource based upon whether they're an admin or the resource owner, we would describe it in English as: "There are two way to be authorized, you are either an admin, or you are the document owner.  If none of these, you're not authorized".  The resulting code would be written to follow this, even if that results in `if` conditionals that may contain empty bodies.
- The keywords and phrases used in the plain English description can often identify subproblems that can be extracted from the main logic.
- If you can't describe the problem or your design in words, something is probably missing or undefined. Getting a program (or any idea) into words can really force it into shape.
- This method of describing the program in plain English is often used when debugging code, where it's known as "rubber ducking".

## Chapter 13 - Writing Less Code
- The most readable code is no code at all.  Every line of code you write is a line of code that must be tested and maintained.  Reusing libraries or eliminating features can save time and keep a codebase lean.
- Keep your codebase as small and lightweight as possible. The larger the codebase, the more complexity it contains.  Create as much generic "utility" code as possible to remove duplication, remove unused code and unused or useless features, keep the project compartmentalized into disconnected subprojects.
- Rethink requirements to solve the easiest version of the problem that still gets the job done.
- Make sure to re-familiarise yourself every so often with the modules, types and methods if your language's standard library. The goal isn't to memorize it, but to ensure you have a sense of what's available.  Leveraging code from the standard library means that's code you don't have to write yourself.

## Chapter 14 - Testing And Readability
- Test code should be just as readable as other code.  When test code is big and scary, coders are afraid to modify the real code and are afraid to add new test code.
- Test code should be written to hide less important details from the reader and to highlight the more important details of the code being tested.
- Using techniques to convert our test code intentions to plain English, we can often boil down most tests to a single line - _for this input/situation, expect this output/behaviour_.
- When reducing test code to one or two function calls, ensure that assertion against the test outcome display sufficiently clear error messages.  Use a better Assertion library if required, or even write your own hand-crafted error messages.
- When choosing input values for tests, try to choose the simplest set of values that completely exercise the code.
- If using a large number of inputs to stress-test some code, it's better to construct those inputs programmatically instead of expressing them literally as this would result in difficult to read test code.
- Use descriptive names for your test functions.  Don't be afraid of having long function names and ensure you capture the class, function and situation being tested and its expected output.
- Practice test-friendly development.  You can perform test-driven development (TDD), but even without TDD, if you write your real code knowing that you'll be writing tests for it later, you start to design your code so that it's easier to test.
- Of all the ways to break up a program into classes and methods, the most decoupled ones are usually the easiest to test.
- Don't go too far with test code.  You shouldn't sacrifice readability of real code for the sake of tests. Don't strive for 100% test coverage as this results in diminishing returns and don't let testing get in the way of product development - don't let it dominate the entire project.

## Chapter 15 - Designing And Implementing A "Minute/Hour Counter"
- We use this chapter to build a class using the techniques from the book.  The class is a "Minute & Hour Counter" and will keep track of the number of bytes transferred by a web server in the last minute and the last hour. 
- The initial class interface for our MinuteHourCounter looks like this:
```
class MinuteHourCounter {
    public:
    // Add a count
    void Count(int num_bytes);
    // Return the count over this minute
    int MinuteCount();
    // Return the count over this hour
    int HourCount();
};
```
- The name of `Count()` could be better.  Count can be both a noun and a verb and it's not clear what the method actually does.  Alternatives could be `Increment()`, `Observe()`, `Record()` or `Add()`.  Record is a noun and verb like Count and the others are all a bit vague.
- Our comments can be improved too.  This comment: `// Add a count  void Add(int count);` is now redundant and would be better is improved to add clarification. e.g. `// Add a new data point (count >= 0).  void Add(int count);`
- Other comments are also unclear.  Consider this: `// Return the count over this minute  int MinuteCount();`.  This could be interpreted as the count over the current clock minute or the count over the last 60 seconds.  Use a better comment such as `// Return the accumulated count over the past 60 seconds.  int MinuteCount();`
- Get an outside perspective on things.  Asking your colleagues and co-workers if a name or comment makes sense and is unambiguous is a great way to test if your code is "user-friendly".
- The initial implementation is naive.  The `Add()` method adds byte counts, but is unbounded - throughout the lifetime of the class, the internal list will continue to grow causing memory pressures.  `MinuteCount()` and `HourCount()` are too slow as they have to examine the list with every invocation.  It would be better for performance to have these methods read directly from pre-computed values that are kept up to date by the `Add()` method.
- One way to fix the problems is to implement a "conveyor belt" design.  We could have two lists, one for last minute and one for last hour which have items removed from them when they're older than the maximum time of the list.  This is inefficient, however, as we need two copies of each event.  A better implementation is a single list, with a two-stage design having the first stage the first minute and the second stage being the hour minus the first minute).  This is implemented by having two lists, and having a method that can "shift" items from one list to the other as time passes.  Minute counts come from the minute only list whilst hour counts count items from both lists.
- This design works, but is very inflexible.  e.g. We're stuck with 1 minute and 1 hour timeslots and can't easily change them.   Also, depending upon how often the `Add()` method is called, this design can use an unbounded and unpredictable amount of memory.
- The new design will improve upon this and a "time-bucketed" design.  This means we have a number of buckets, say one bucket for each minute in the past 60 minutes. All events that fall into the boundaries of a given buckets minute are grouped together.  When we need to count, we simply sum the totals from each bucket required.  Whilst this design can lose some precision, we gain a fixed, predictable memory usage.  We can always improve precision by having more buckets of smaller, more granular time periods.
- This final design solved the previous problems by breaking things down into subproblems. Here are the three classes we created, in bottom-up order, and the subproblem each one solved: `ConveyorQueue`: A maximum-length queue that can be "shifted" and maintains its total sum.  `TrailingBucketCounter`: Moves the ConveyorQueue according to how much time has elapsed and maintains the count of a single (latest) time interval, with a given precision.  `MinuteHourCounter`: Simply contains two TrailingBucketCounters, one for the minute count and one for the hour count.

