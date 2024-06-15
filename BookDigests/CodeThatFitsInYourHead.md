# Book Digest: Code That Fits In Your Head: Heuristics for Software Engineering

Title     : Code That Fits In Your Head: Heuristics for Software Engineering 
Author(s) : Mark Seemann  
ISBN-10   : 0137464401  
ISBN-13   : 978-0137464401

## Chapter 1: Art or Science?
- Building a House vs. Growing a Garden: Software development is often mistakenly treated like a linear process (building a house) but is more akin to an iterative, evolving process (growing a garden).
- Towards Engineering: Introduces heuristics as practical rules to guide software development, aiming to balance the artistic and scientific aspects of programming.

## Chapter 2: Checklists
- Aid to Memory: Checklists help prevent errors by ensuring no steps are forgotten, crucial in complex tasks like software development.
- Checklist for a New Code Base: Recommends starting with version control (Git), automating the build process, and ensuring comprehensive error logging.
- Adding Checks to Existing Code Bases: Advises on incrementally integrating checklists into existing projects to improve quality and consistency.

## Chapter 3: Tackling Complexity
- Purpose of Software: Software should be sustainable and provide value, focusing on long-term maintenance and usefulness.
- Why Programming Is Difficult: Discusses cognitive challenges, the need for readable code, and the intellectual demands of programming.
- Towards Software Engineering: Advocates for humane code that considers human factors, aligning software development practices with computer science principles.

## Chapter 4: Vertical Slice
- Start with Working Software: Introduces the concept of a minimal vertical slice, a complete end-to-end feature that ensures a functional starting point.
- Outside-In Development: Steps to implement a feature slice, starting from external interfaces (like JSON handling) and working inward (configuring dependencies).
- Complete the Slice: Ensures all components, including the database schema and repository configurations, are in place and functional.

## Chapter 5: Encapsulation
- Save the Data: Emphasizes the Transformation Priority Premise, prioritizing transformations that are easier to implement and understand.
- Validation: Strategies for ensuring data correctness, including validating inputs and handling edge cases.
- Protection of Invariants: Ensures the system maintains valid states, protecting critical data rules and constraints.

## Chapter 6: Triangulation
- Memory and Legacy Code: Discusses the impact of cognitive load and memory on working with legacy code, highlighting the need for effective memory management.
- Capacity Management: Introduces overbooking and the Devil's Advocate technique to balance system capacity and quality.
  - Overbooking: The practice of planning for more tasks than can be realistically completed to ensure continuous productivity.
  - Devil's Advocate: A role or technique used to challenge ideas and assumptions to improve decision-making and problem-solving.

## Chapter 7: Decomposition
- Code Rot: The gradual deterioration of code quality over time due to increasing complexity and lack of maintenance.
- Cyclomatic Complexity: A metric that measures the number of linearly independent paths through a program's source code, indicating its complexity.
  - 80/24 Rule: A heuristic suggesting that 80% of code quality issues can often be traced back to 24% of the codebase.
  - Code That Fits in Your Brain: Techniques to keep code cohesive, minimize feature envy, and ensure it remains manageable and comprehensible.

## Chapter 8: API Design
- Principles of API Design: Key principles include:
  - Affordance: Designing APIs that are intuitive and easy to use.
  - Poka-Yoke: Error-proofing APIs to prevent misuse.
  - Command-Query Separation: Distinguishing between operations that change state (commands) and those that return data (queries).

## Chapter 9: Teamwork
- Git and Commit Messages: Stresses the importance of clear and descriptive commit messages for effective collaboration.
- Collective Code Ownership: Encourages practices like pair programming and mob programming to ensure all team members are familiar with the codebase.
- Regular Code Reviews: Promote shared understanding and adherence to coding standards.

## Chapter 10: Augmenting Code
- Feature Flags: Use feature flags to manage the release of new features safely, allowing for gradual rollout and easy rollback.
- Strangler Pattern: A technique for incremental system replacement, gradually phasing out legacy components by adding new functionality alongside the old system.

## Chapter 11: Editing Unit Tests
- Refactoring Unit Tests: Strategies for updating test code to reflect changes in production code without breaking tests.
- See Tests Fail: Emphasizes the importance of observing test failures to ensure tests are effective and reliable.

## Chapter 12: Troubleshooting
- Understanding and Simplifying: Uses methods like rubber ducking (explaining code to an inanimate object) to clarify and simplify problem-solving.
- Defects and Bisection: Techniques for isolating and reproducing defects, including using bisection with Git to find the source of bugs.
  - Bisection: A method of systematically narrowing down the source of a bug by checking halfway points in the code history.

## Chapter 13: Separation of Concerns
- Composition: Strategies for composing software components to maintain separation of concerns.
- Cross-Cutting Concerns: Techniques for handling concerns that affect multiple parts of the system, such as logging and error handling.

## Chapter 14: Rhythm
- Personal and Team Rhythm: Time management practices like time-boxing, taking regular breaks, and keeping dependencies up-to-date to maintain a sustainable work pace.
  - Time-Boxing: Allocating fixed time periods to activities to ensure focused and efficient work.

## Chapter 15: The Usual Suspects
- Performance and Security: Addresses common issues in software development, including performance optimization and security threats.
  - STRIDE Model: A framework for identifying security threats, including Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, and Elevation of privilege.

## Chapter 16: Tour
- Learning from Tests: Encourages using tests as a learning tool to understand code behaviour and improve quality.

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

