# Book Digest: Code That Fits In Your Head: Heuristics for Software Engineering

Title     : Code That Fits In Your Head: Heuristics for Software Engineering 
Author(s) : Mark Seemann  
ISBN-10   : 0137464401  
ISBN-13   : 978-0137464401

## Chapter 1 - Art Or Science?
- Software Development is much more art than it is science.
- Although we often hear the term "Software Engineering", software bears very little resemblance to actual engineering practice in other fields.
- Despite software lacking true engineering rigour, there are many practices that can be adopted to make software development more like engineering.

## Chapter 2 - Checklists
- A fundamental problem with Software Development is that there's always a lot going on and our brains aren't great at keeping everything in memory.
- To ensure that important items don't get forgotten, use checklists, especially at the beginning of a project.
- A good checklist for a new project might be:
  - Use Git version control
  - Automate the build
  - Turn on all error messages (treat warnings as errors)
- It's rare that we can start entirely new projects, but checklists like the above can also be used with existing codebases as part of a gradual improvement process.

## Chapter 3 - Tackling Complexity
- It's said that humans have a limited capacity of holding current information in memory - the number of items is said to be 7.
- Software Development must provide value to the organisation that creates it, but that development must also be sustainable over time.
- Optimize your code for reading, not writing.  Code is read far more often than it's written.
  - Code should be readable, ideally like prose.
  - Helps to ensure that new programmers to the codebase, or even a future you, can understand the code's intention.
- Code isn't an asset, it's a liability.  The faster you type, the more code you create that has to be maintained.
- It's only by applying good architecture and engineering disciplines that the sustainability of software development can be maintained.

## Chapter 4 - Vertical Slice
- Software usually has many horizontal layers.  These start at the user-interface, then go all the way through to the data store.
- Vertical slices are implementations of some small piece of functionality of the software that is implemented within every horizontal layer.
- Start new projects with a walking skeleton, which is the minimal amount of code that encompasses every horizontal layer of the code.
- You should always find a motivation for making changes to code.  Such motivation acts as a _driver_ of the change.
  - Drivers gave rise to many types of x-driven software techniques such as Test-Driven Development, Behaviour-Driven Development, Domain-Driven Design etc.
- Thin vertical slices are an effective way to demonstrate that the feature actually works.  When combined with Continuous Delivery, you can very quickly get working software into production.

## Chapter 5 - Encapsulation
- Encapsulation is an important part of making code readable and understandable.
- Encapsulation is not primarily about hiding an object's private data and only exposing it through property getters, it's primarily about ensuring that the object "protects its invariants".  This means that the object is always in a valid state.
- The essential quality of an object is its contract. It's usually simpler than the underlying implementation, so it fits better in your brain.
- Postel's law states, "Be conservative in what you send, be liberal in what you accept".
  - This can be interpreted as allowing input as long as you can meaningfully work with it, but no longer.
  - A corollary is that while you should be liberal in what you accept, there’s still going to be input you can't accept. As soon as you detect that that's the case, fail fast and reject the input.
- You can use the [Transformation Priority Premise](https://blog.cleancoder.com/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html), which provides a set of heuristics of how to make refactorings to existing code, as a driver for code change.
- The interaction between an object and a caller should obey a contract.  This is a set of pre- and postconditions.
  - The preconditions describe the responsibilities of the caller. If the calling code fulfils those obligations, however, the postconditions describe the guarantees given by the object.
- Use the Red-Green-Refactor cycle of Test-Driven Development to help guide the specific changes to your code.
  - It's one of the most scientific methodologies of software engineering as you first form a hypothesis (a failing test), then perform an experiment and compare the outcomes (making the test pass and refactoring code if necessary).
  
## Chapter 6 - Triangulation
- Short-term memory has a much smaller capacity than long-term memory.
- When working with legacy code, you have to slowly and painstakingly commit the code and its structure to long-term memory however, there's two problems in doing this:
  - It takes a long time to learn the codebase.
  - Change is difficult.  This is because changes to the structure of the code are hard to change from the previously committed structure within your long-term memory.
- Use tests to cover the desired behaviours of your codebase.
- Use the "Devil's Advocate" technique to help answer the question of knowing if you have sufficient test cases.  This involves deliberately trying to make tests pass by using a known-incomplete implementation.  If a test passes that should really fail, you're missing a test case.
- Don't forget about the Red-Green-Refactor cycle of test-driven development. As you make additional test cases pass, remember to refactor the implementation code to be more readable and understandable.
- When you test-drive a codebase, the tests play the role of measurements.  When you add a failing test, you're measuring something that doesn't yet exist.
- The more tests you add, the better, and more precisely, you describe the system under test, just as more measurements in (for example) a geographic survey produces a more accurate and precise result.
- Always write numeric expressions in "number-line order". For example, if you need to check if some variable is between a defined minimum and maximum value, write the comparison like so:  `min <= [variable] <= max`.  This help readability as the min and max are in their most natural positions - minimum on the left and maximum on the right.
- To determine when you have enough tests, you should consider the likelihood of a regression in the code under test.  For example, if the code is a method clearly named to compute a sum of some values, and you've used the `.Sum` LINQ method within the code, it's unlikely that a programmer will change that to something else.

## Chapter 7 - Decomposition
- No one sets out to write legacy code, but code bases will naturally and gradually deteriorate.
  - Code bases gradually become more and more complicated through a series of small changes and when programmer's aren't paying sufficient attention to the overall quality.
- Institute a rule or metric on your team to examine some aspect of code quality.  Ensure that any code changes that violate the metric are rejected.
  - One good starting metric is cyclomatic complexity of each method.  Pick a value, for example, 7 - to align with the number of things you can keep in your head at once - and enforce code to not violate that rule.
  - Cyclomatic Complexity is one of very few code metrics that have universal usefulness.  It's a measure of the number of pathways through a piece of code.
- Keep methods short.  
  - Follow the 80/24 rule.  This rule is named after the approximate number of characters (80) and lines of text (24) that can fit on a single screen (using old fashioned VDU sizes) without any scrolling. This rule is not a hard and fast one and is more of a guide.
  - In line with the rule regarding keeping only 7 things in your brain at once, ensure methods have no more than 7 things going on within them.
- As you add methods to classes, ensure that there is _cohesion_ between the methods.  Cohesion means that things that change together should be kept together and, conversely, things that change at different rates belong apart.
- Use careful abstractions when designing classes and methods.  Abstraction can be thought of as the "elimination of the irrelevant and the amplification of the essential".
- When refactoring code, beware of "feature envy".  This is a code smell where some code exists in one place, but the code accesses methods or objects elsewhere more than it accesses methods in it's own class.  Refactor to move the method to the object that the method seems "envious" of.
- Beware of code that can lose information.  A simple `IsValid` property or method might return a boolean flag to indicate validity (or not) however, downstream code often needs to know _why_ something may not be valid.  It may be better to return an object that contains both the validation result as well as reasons for validation failure (if applicable).
- Avoid methods that return an object, in the case of success, but null, in the case of failure. (i.e. a `Validate()` method might do this).
  - Use the `Option<T>` (aka `Maybe<T>`) monad to "wrap" the return object forcing callers to the method to explicitly handle both cases.  The success case where the object `T` is returned and the failure case where it is not.
- You should aim for an architecture of your code base so that regardless of where you look, the code fits in your head. At a high level, there's 7 or fewer things going on. In the low-level code, there's at most 7 things you have to keep track of. At the intermediary level, this should continue to hold.

## Chapter 8 - API Design
- An API is a contract with the outside world.  The interface of your API offer the consumer _affordance_.  Affordance is the set of methods, values, functions, and objects exposed via the API.
  - The affordance should be a good abstraction over the features and functionality that your API provides.  It's an API that is intuitive and easy to use.  The API should also provide sufficient encapsulation to ensure that object invariants are protected.
- Good API Design follows some key principles










## Chapter 9 - Teamwork

## Chapter 10 - Augmenting Code

## Chapter 11 - Editing Unit Tests

## Chapter 12 - Troubleshooting

## Chapter 13 - Separation Of Concerns

## Chapter 14 - Rhythm

## Chapter 15 - The Usual Suspects

## Chapter 16 - Tour







## Appendix A - List Of Practices

### The 50/72 Rule
- Write conventional Git commit messages.  Keep all lines to a maximum of 72 characters long.  The first line should be an imperative summary with a blank line following and any further comments added after the blank line.

### The 80/24 Rule
- Write small blocks of code.  Try to keep code in blocks of 80 horizontal characters and 24 lines as this corresponds to an old terminal window.  Don't stick to this too rigidly, but use it as a guideline.

### Arrange Act Assert
- Structure automated tests according to the Arrange Act Assert pattern to make it clear to readers where one section ends and the next begins.

### Bisection
- When debugging code, try to remove half of the code and see if the problem is still present.  This let's you know which half of the code the problem is in.  Repeat halving code until the problem is narrowed down to a minimal working example.
- Remember that [Git](https://git-scm.com/) contains the `bisect` command which will perform the same action across multiple commits.

### Checklist For A New Codebase
- When creating a new codebase, always start with a known checklist of items to implement.
- The items can be chosen based on your project's specific needs but an example might be:
  - Use Git
  - Automate the build
  - Turn on all error messages (Enable treating warnings as errors)

### Command Query Separation
- Separate Commands from Queries. Every method should be either a Command or a Query, but not both.
- Commands are procedures that have side effects. Queries are functions that return data.

### Count The Variables
- Count all the variables involved in a method implementation and try to keep the number as low as possible.  Be sure to include both local variables, method parameters, and class fields.

### Cyclomatic Complexity
- Cyclomatic complexity measures the number of pathways through a piece of code, thereby giving you an indication about the complexity of a method.
- Try to keep the Cyclomatic complexity of every method to 7 or below.
  - 7 is a good number as it corresponds with the [amount of items an average human can hold in their head at once](https://en.wikipedia.org/wiki/The_Magical_Number_Seven,_Plus_or_Minus_Two).
- The number also gives you the minimum number of test cases you have to write to fully cover a method.

### Decorators For Cross-Cutting Concerns
- Use the [Decorator design pattern](https://en.wikipedia.org/wiki/Decorator_pattern) to add cross-cutting concerns such as logging, caching, authorisation etc. to your business logic.
- For example, if you have an `IRepository` and an implementation called `SqlRepository`, don't add logging concerns to `SqlRepository`, create a `LoggingSqlRepository` that implements the `IRepository` interface but also "wraps" an instance of `SqlRepository` within it.  Add the logging to `LoggingSqlRepository` and call the same methods on `SqlRepository` to perform the actual data access.

### Devil's Advocate
- The Devil's Advocate technique is used in unit testing and involves deliberately implementing the System Under Test incorrectly.  The more incorrect you can make it, the more test cases you should consider adding.
- You can use it to review existing (test) code, but you can also use it as inspiration for new test cases that you should consider adding.
- Some "Mutation Testing" tools (such as [Stryker](https://stryker-mutator.io/)) can automate this technique.

### Feature Flag
- If you can't complete a coherent set of changes in half a day's work, hide the feature behind a [feature flag](https://martinfowler.com/articles/feature-toggles.html), and continue to integrate your changes with other peoples' work.

### Functional Core, Imperative Shell
- Favour pure functions.  Pure functions can be composed together easily and are easier to unit test.
- Keep code that deals with inherently mutable state (dates, database values, console input and other ephemeral environmental state) at the outside edges of your program.

### Hierarchy Of Communication
- Write your code with future readers in mind.  They could be someone else or even you.
- Guide the reader by:
  - Giving API's distinct types
  - Giving Methods descriptive, helpful names
  - Writing good comments
  - Providing illustrative examples as automated tests
  - Writing helpful commit messages in Git
  - Writing good documentation

### Justify Exceptions From The Rule
- Have rules to follow when developing code, but don't force compliance if it will create other problems.
- It's okay to deviate from a rule when circumstances require it, but justify and document the reason.

### Parse, Don't Validate
- Convert less-structured data to more-structured data as soon as possible, for example, when receiving JSON/XML data as input.
- Use a data structure that makes illegal states unrepresentable, thereby ensuring that you don't need to invoke separate validation functions to ensure correctness.

### Postel's Law
- Be conservative in what you send, be liberal in what you accept.
- In essence, this means: Methods should accept input as long as they can make sense of it, but no further. Return values should be as trustworthy as possible.

### Red Green Refactor
- When engaging in test-driven development, ensure you follow the red-green-refactor cycle.
  - Write a failing test
  - Make all tests pass by doing the simplest thing that could possibly work.
  - Consider the resulting code and make improvements where available.  Consider using [Connascence](https://en.wikipedia.org/wiki/Connascence) or the [Transformation Priority Premise](https://en.wikipedia.org/wiki/Transformation_Priority_Premise) to guide you in your refactoring efforts.

### Regularly Update Dependencies
- Check for updates to dependencies (i.e. NuGet packages, Framework versions etc.) at a regular interval and don't fall too far behind with versions/updates.

### Reproduce Defects As Tests
- Whenever you encounter a bug, try to reproduce that bug as an automated test (e.g. failing unit test).
- Fixing the bug makes the test pass and the continued existence of the test helps to ensure that same bug does not reappear.

### Review Code
- Always have another person review code that you write as it's one of the most effective quality assurance techniques we know of.
- Code reviews can be performed asynchronously as pull request reviews or continually during a pairing or mobbing session.

### Semantic Versioning
- If possible, use [Semantic Versioning](https://semver.org/).

### Separate Refactoring Of Tests And Production Code
- Automated tests give you confidence when you need to refactor your production code, however, refactoring test code, is more dangerous because you have no automated tests of the tests.
- Don't try to refactor production code and test code at the same time, only refactoring one type of code at once, using the other as a "pivot".
- When refactoring test code, do so very carefully as you no longer have any "safety net" to guide you.

### Slice
- Work in small increments where each increment improves a running, working system.
- Use vertical slices to add new functionality.  A Vertical slice cuts through all conceptual layers of the application, from UI to data storage.

### Strangler
- Use the [Strangler pattern](https://en.wikipedia.org/wiki/Strangler_fig_pattern) when making big refactoring changes to a system.
- Establish the new way of doing things side-by-side with the old way, and gradually migrate code from the old to the new way.
  - Note that this process can take many hours, days or even weeks, but during the migration process, the system is always consistent and stable.
  - When no code calls the original API, you can delete it.

### Threat Model
- Take deliberate security decisions.
- Use the [STRIDE model](https://en.wikipedia.org/wiki/STRIDE_model) to help identify security threats.

### Transformation Priority Premise
- Always try to work in a way so that your code is in a valid state most of the time.
- Transitions from one valid state to the next usually involve a phase where the code is in an invalid state, but try to minimise the length of time of this invalid state.
- Use the [Transformation Priority Premise](https://en.wikipedia.org/wiki/Transformation_Priority_Premise) to suggest each small series of transformations of the code that minimises the invalid states.

### X-Driven Development
- Use a _driver_ for the code that you write.  A driver can be a unit test, static code analysis, built-in refactoring tools of the IDE etc.
- It's okay to deviate from this rule, but the closer you adhere to it, the less you tend to go astray.

### X Out Names
- Temporarily replace method names with X's to examine how much information a method's signature communicates.  You can do this in your head, you don't have to do it in the editor.
- If a method's intentions are unclear when the name is removed, consider refactoring the method to introduce more expressive and descriptive types in the signature (both for inputs and output).
- This makes most sense in a statically-typed language.  In these languages, types can carry a lot of information if you design them so.

