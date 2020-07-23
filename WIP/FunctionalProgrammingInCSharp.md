# Book Digest: Functional Programming In C#

Title     : Functional Programming In C#  
Author(s) : Enrico Buonanno
ISBN-10   : 1617293954  
ISBN-13   : 978-1617293955

## Chapter 1 - Introducing Functional Programming
- At a high level, Functional Programming is a programming style that emphasizes functions whilst avoiding state mutation.
- In the functional paradigm, functions are considered first-class values within the language and can be used anywhere a variable or literal value can be used.  Importantly, they can be used as inputs or outputs to other functions.
- In the functional paradigm, we avoid state mutation.  This means that once created, an object never changes or a variables value never changes.  Such changes are _destructive_ updates as we lose the value that was previously there.  To follow this principle, when an object needs to change to reflect a new value, we simply return a whole new object.
- State mutation is problematic as it's not thread-safe.  If you have multiple threads or processes reading and writing the same piece of state errors and inconsistencies can occur.  This means that concurrency cannot easily be achieved in programs that mutate state.  When a program is written in a function style and avoids state mutation, concurrency can often be safely added for free.
- Support for functions is pretty good in C#. It's been there for some time, starting with the `delegate` type, but today is more frequently found in the form of lambda expressions.  Because we avoid state mutation and create new objects, the language ideally needs good garbage collection and here, C# satisfies this requirement well.
- A good functional language should discourage in-place mutation of state.  Unfortunately, in C#, everything is mutable by default and this is C#'s biggest short-coming as a functional language.
- One of the best things to come in the C# language from a functional perspective is LINQ.  Methods such as `Where`, `OrderBy`, `Select` etc. all take functions as arguments and don't mutate the given `IEnumerable` upon which they operate.
- C# 6's `using static` statement allows importing the static members of a class meaning we can refer to those members without having to prefix them with the class name.  e.g. `using static System.Math;  public double Circumference => PI * 2 * Radius;`.
- This is important as, in functional programming, we prefer functions whose behaviour relies solely upon their input values.  Instance methods typically interact with instance variables - an example of shared state.
- C# now also has getter-only auto properties whose values can only be set from the constructor:
    ```
    public class Circle
    {
        public Circle(double radius) => Radius = radius;
        public double Radius { get; }
    }
    ```
    These facilitate the definition of immutable types.
-  In mathematics, a function is a map between two "sets", respectively called the domain and codomain.  That is, given an element from its domain, a function yields an element
from its codomain.  The value that a function yields is determined exclusively by its input.
- In programming, these "sets" are represented by types.  If the domain was all the lower case letters of the alphabet and the codomain was the upper-case letters, we could use `char` to represent both the domain and the codomain.  The type of function that translates between them would them be written like: `char => char`.  That is, given a `char`, the function will yield a `char`.
- There are several language features in C# that allow us to represent functions: `Methods`, `Delegates`, `Lambda Expressions`, `Dictionaries`.  Dictionary are usually thought of as data, but they can represent functions where each input value (the dictionary "key") has a resulting output value (the dictionary "value").
- C# delegate used to be expressed with the `delegate` keyword, e.g. `public delegate Greeting Greeter(Person p);` however, now C# contains built-in `Func` and `Action` types to represent delegates (e.g. `Func<Person, Greeting>`) so the previous way of declaring delegates is rarely used.
- Functions have what's known as an "arity".  This is the number of arguments that a function accepts.  A "nullary" function takes no arguments.  A "unary" function takes 1 argument. A "binary" functions takes 3 arguments and a "ternary" function takes 4 arguments.
- Lambda Functions (usually just called "lambdas"), have access to the variables in the scope in which they’re declared.  When such a variable is "captured" by the lambda expression, this is referred to as a "closure".
- One of the most important benefits of having functions as first-class values is the ability to define Higher-Order Functions (HOF's).  These are functions that accept other functions as input, or yield functions as results.
- A good example of built-in HOFs are the `List.Sort` method, which takes a delegate to determine how to compare the items in the list for sorting, or the LINQ `Where` method, which takes a lambda expression to determine how the items in the `IEnumerable` should be filtered.
- Both of the above examples are _iterated applications_.  That is, the provided delegate function is invoked (or "applied") to every element in the collection.
- One of the most common patterns for HOFs is sometimes referred to as inversion of control: the caller of the HOF decides what to do by supplying a function, and the function decides when to do it by invoking the given function.
- Some HOFs don't _apply_ the given function, but return a new function instead.  e.g. If you had a function to divide two numbers: `Func<int, int, int> divide = (x, y) => x / y;` you might want to change the order of the arguments.  This can be achieved with an _adapter function_: `static Func<T2, T1, R> SwapArgs<T1, T2, R>(this Func<T1, T2, R> f) => (t2, t1) => f(t1, t2);`.  Now instead of calling `divide(10,2)` we can do: `var divideBy = divide.SwapArgs();  divideBy(2,10);`
- You can create functions that exist only to create other functions.  You could create a general purpose function such as: `Func<int, bool> isMod(int n) => i => i % n == 0;` which would create the predicate required to filter a list by only modulo. e.g. `Range(1, 20).Where(isMod(2));` or `Range(1, 20).Where(isMod(3));`.
- Another common use case for HOF s is to encapsulate setup and teardown operations.  For example, interacting with a database requires some setup to acquire and open a connection.  Instead of writing:
    ```
    using (var conn = new SqlConnection(connString))
    {
        conn.Open();
        // interact with the database...
    }
    ```
    We could write:
    ```
    public static R Connect<R>(string connString, Func<IDbConnection, R> f)
    {
        using (var conn = new SqlConnection(connString))
        {
            conn.Open();
            return f(conn);
        }
    }
    ```
    And this above function could be called in the following manner: `Connect(connString, c => c.Execute("sp_create_log"));`.  What we're doing is effectively "abstracting away" the ceremony of the using statements setup and teardown logic.  We can create an even more generic function which is truly reusable for all need of the `using` statement:
    ```
    public static R Using<TDisp, R>(TDisp disposable, Func<TDisp, R> f) where TDisp : IDisposable
    {
        using (disposable) return f(disposable);
    }
    ```
    Now, we can use this Using function anywhere where we'd otherwise use a `using` statement: `Using(new SqlConnection(connString), conn => { conn.Open(); // Do some db work; });`
- Note the the Using function above is an _expression_ rather than a _statement_.  Fundamentally, expressions return a value, statements don't.
- HOFs do have some drawbacks.  They usually increase stack use, so calls to the "innermost" function can be more stack frames apart than the equivalent code written without using HOFs.  There's a performance impact to this, but it's usually negligible.  This also means that debugging can be a bit more complex due to the callbacks that occur when nesting functions inside HOFs.
- Use HOFs when appropriate, but be mindful of readability: use short lambdas, clear naming, and meaningful indentation.

## Chapter 2 - Why Function Purity Matters
- Functions can be "pure" or "impure".  Mathematical functions are considered "pure" as they do nothing but return a computed value based on inputs.  They also have no context of the state of anything around them, so they are entirely self-contained.  In programming, many of our functions are "impure" as they do more than simply return a value, but may exhibit "side-effects", such as printing something to the screen, writing to a file or sending an HTTP request over the network.  They also have access to a context which may include instance variables, variables captured by closures as well as other elements outside the scope of the function or program, such as the system clock.
- A function is considered pure only if it has no side-effects.  Side-effects are:
    - Mutating global state - changing state that is outside the scope of the function.
    - Mutating input arguments - any changes to the input arguments of a function is considered a side-effect.
    - Throwing exceptions - An exception breaks "normal" program flow and introduces indeterminism into the function.
    - Performing any I/O operations - This includes any interaction between the program and the outside world, such as reading or writing to the console, the filesystem, a database etc.
- Pure functions are deterministic.  This means that invoking the function with the same inputs always produces the same output.  This has some positive benefits such as:
    - Reasoning - Pure functions are easy to test and easy to reason about and can be algebraically proven to be correct.
    - Parallelization - Pure functions make parallelization of work much easier.
    - Lazy evaluation - Pure functions allow for evaluation of expressions only as needed.
    - Memoization - Pure functions allow caching of a function result so that it's only computed once.
    These techniques can also be achieved with impure functions, however, it's much more difficult 
- Given the list of side-effects above, it's almost impossible to write an entire program consisting of pure functions.  Any real-world application will require some or all of those side-effects so we need strategies to isolate the side-effects to allow as much of our program to remain as pure as possible.
- The strategy for keeping programs as pure as possible is to isolate the impure parts of the program from the pure functions.  In doing this, the impure functions can call pure functions, but pure function can never call impure functions else they themselves become impure.
- Pure functions parallelize well and are generally immune to the issues that make concurrency difficult, which is largely related to state mutation.
- Concurrency is the general concept of having several things going on at the same time, however concurrency can mean multiple things.  Asynchrony is one type of concurrency and refers to the program being able to perform non-blocking operations - e.g. it can initiate a HTTP request and then do some other task whilst waiting for the response.  Parallelism is another type of concurrency and refers to the ability of your program to execute tasks at the same time by breaking up work into separate tasks, each of which is executed on a separate CPU core.  Multithreading is yet another type of concurrency and refers to a software implementation that allows different threads to be executed concurrently.  This can still happen on a single core machine by switching back and forth, but it appears that multiple tasks are happening at the same time.
- Unlike pure functions, whose application can be parallelized by default, impure functions don't parallelize out of the box. And because parallel execution is nondeterministic, you may get some cases in which your result is correct and others in which it isn't resulting in hard to trace bugs.
- When all variables required within a method are provided as input (or are statically available), the method can be made static.  Although static classes/methods have previously been frowned upon as programs can become difficult to test and maintain due to excessive use, when a method is pure it can be made static with no problems and with no impact to testability.
- To test impure functions, e.g. one that performs date validation using the current system date, we would use an "interface-based approach" in our object-oriented code:
    ```
    public interface IDateTimeService
    {
        DateTime UtcNow { get; }
    }
    public class DefaultDateTimeService : IDateTimeService
    {
        public DateTime UtcNow => DateTime.UtcNow;
    }
    public class DateNotPastValidator : IValidator<MakeTransfer>
    {
        private readonly IDateTimeService clock;
        public DateNotPastValidator(IDateTimeService clock)
        {
            this.clock = clock;
        }
        public bool IsValid(MakeTransfer request) => clock.UtcNow.Date <= request.Date.Date;
    }
    ```
    Whilst this works, there is a lot of boilerplate code required and such an approach can lead to an explosion of interfaces inside the code base.  Also, despite having the date required for validation injected into our Validator class, we still can't prove that the function is pure as it depends on the implementation of the `IDateTimeService` that's injected.  Our test class would use a "fake" implementation that returns the same date every time, thus making it pure, but the "real" production code would likely use an impure implementation.  We can improve this to use a function signature rather than a complete interface:
    ```
    public class DateNotPastValidator : IValidator<MakeTransfer>
    {
        private readonly Func<DateTime> clock;
        public DateNotPastValidator(Func<DateTime> clock)
        {
            this.clock = clock;
        }
        public bool IsValid(MakeTransfer request) => clock().UtcNow.Date <= request.Date.Date;
    }
    ```
    This is less code, but we still don't know if our function is pure as we don't know the implementation of the `clock` function that's injected.  We could improve this even further by injecting only a _value_ instead of injecting an entire interface:
    ```
    public class DateNotPastValidator : IValidator<MakeTransfer>
    {
        private readonly DateTime today;
        public DateNotPastValidator(DateTime today)
        {
            this.today = today;
        }
        public bool IsValid(MakeTransfer cmd) => (today <= cmd.Date.Date);
    }
    ```
    This results in much less code and actually makes the `IsValid` function pure as the `today` argument is no longer mutable.  Downsides to the previous implementations taking either a `Func` or a value are that the caller of the function now needs to understand what kind of function or date should be passed, thus bleeding some of the logic of the function to the outside world.
- To test pure functions, the unit is the function itself and since pure functions rely only on the function inputs for their output and also produce the exact same output for a given input, testing is easy.
- In this respect, impure functions rely on their inputs and the "state of the world" in order to produce a given output.  Pure functions rely only on their inputs in order to produce a given output.
- We can see that function purity matters a great deal.  The evolution of software and hardware also has important consequences for how we think about purity. Our systems are increasingly distributed, so the I/O part of our programs is increasingly important and the ability to more easily parallelize our programs and deal with concurrency means that functional programming will gain in importance.

## Chapter 3 - Designing Function Signatures And Types
- There's a notation for function signatures that's standard within the functional programming community.  It's called arrow notation.  For example, a function that takes an `int` as an input and returns a `string` would be written as:
    ```
    f: int => string
    ```
    In English, we'd read this as "f _has type_ of `int` to `string`".  The equivalent way to express this in C# would be as `Func<int,string>`.  No input or output would be expressed as opening and closing parentheses, i.e. `()`.  This is the same as `void`.
- The following table shows some examples of function signatures using arrow notation, the equivalent C# type and some examples:
    | Function Signature   | C# Type             | Example                        |
    |----------------------|---------------------|--------------------------------|
    | `int` -> `string`    | `Func<int,string>`  | `(int i) => i.ToString();`     |
    | `() => string`       | `Func<string>`      | `() => "hello";`               |
    | `int => ()`          | `Action<int>`       | `(int i) => Writeline($"{i});` |
    | `() => ()`           | `Action`            | `() => Writeline("Hello");`    |
    | `(int, int) => int`  | `Func<int,int,int>` | `(int a, int b) => a + b;`     |
- For the last example above that has multiple inputs, parentheses here are used to indicate tuples, that is, we're notating a binary function (a function taking two inputs) as a unary function (a function taking a single input) whose input argument is a binary tuple.
- When we see a function like this:
    ```
    public static R Connect<R>(string connStr, Func<IDbConnection, R> func)
        => Using(new SqlConnection(connStr), conn => { conn.Open(); return func(conn); });
    ```
    It's signature can be defined as:
    ```
    Func<string, Func<IDbConnection, R>, R>
    ```
    That is, a function that takes a string and another function as input parameters and returns an `R`.  The second input parameter is a function that itself takes an `IDbConnection` as an input parameter and returns an `R`.  The equivalent arrow notation, which is slightly simpler is:
    ```
    (string, (IdbConnection => R)) => R
    ```
- Some function signatures are very expressive, some less so.  A function signature of `() => ()` tells us almost nothing as to what the function actually does, but a function signature of `(IEnumerable<T>, (T => bool)) => IEnumerable<T>` tells us quite clearly that the function is using a _predicate_ (the `(T => bool)` part) to filter the `IEnumerable<T>` input to return a new `IEnumerable<T>`.  Having signatures that are very expressive is a good trait as it allows us to be clear in our intent and almost allows the reader to make a very good guess at the actual function implementation.
- Make your function signatures as specific as possible. This will make them easier to consume and less error-prone.
- Make your functions honest. An honest function always does what its signature says, and given an input of the expected type, it yields an output of the expected type - no Exceptions, no nulls.
- In OOP, we try to avoid "anemic" objects that only contain data, however, in functional programming it's fine to have anemic data objects that only contain data as all of the behaviour and functionality is encoded in functions, which usually live outside of any object or class.
- We should use custom types to constrain inputs to functions.  If we have a function that expects a person's age to be passed in order to calculate an insurance risk profile, i.e. `CalculateRiskProfile(int age)`, we may use an `int` datatype, however, `int`'s can be negative or hold values far beyond that of a reasonable person's age.  Instead of adding validation logic to the actual function itself to check that the `int` is within certain boundaries, it's better to create a custom type that contains those same rules and use that as the input type to the function, i.e. `CalculateRiskProfile(Age age)`.
- Custom types are heavily used in functional programming as they're one of the core tenets of _making invalid state unrepresentable_.
- A function is honest if its behaviour can be predicted by its signature: it returns a value of the declared type; no throwing exceptions, and no null return values.
- The absence of data is often modelled with `void`, however, `void` doesn't work well with functional techniques such as chaining functions and wrapping code as a `Func` inside a method, such as the following that will log the execution time of any `Func`:
    ```
    public static class Instrumentation
    {
        public static T Time<T>(string op, Func<T> f)
        {
            var sw = new Stopwatch();
            sw.Start();
            T t = f();
            sw.Stop();
            Console.WriteLine($"{op} took {sw.ElapsedMilliseconds}ms");
            return t;
        }
    }
    ```
    We use the `Unit` type, which is simply an alias for an empty `System.ValueTuple`, to represent the absence of data.  This is required as the code above would not work if what we want to instrument is an `Action` which does not return a value.  By converting an `Action` to a `Func<Unit>` (i.e. a function that returns "no" value), we can now instrument any code with the above, whether it's a true function returning a value or not.
- Use void to indicate the absence of data, meaning that your function is only called for side effects and returns no information. Use Unit as an alternative, more flexible representation when there's a need for consistency in the handling of `Func` and `Action`.
- We can use the `Option` type to make working with data, or the possible absence of it, much easier.  An `Option` is a container that wraps a value or no value - like a box that may contain something, or it may contain nothing. The symbolic definition for `Option` is: `Option<T> = None | Some(T)`.  `Option` is also called a `Maybe` type in some languages.  An `Option` is an example of a _discriminated union_, a type can can be one of a number of different things.
- Using `Option` means that you can create it and assign either no value or a value. e.g.
    ```
    Option<string> _ = None;
    Option<string> john = Some("John");
    ```
    Code that might need to interact with an `Option`, say as a return type from a function call, is forced to handle both the `Some` and `None` cases by the compiler.  This handling is done using pattern matching. e.g.
    ```
    string greet(Option<string> greetee)
    => greetee.Match(
        None: () => "Sorry, who?",
        Some: (name) => $"Hello, {name}");

    greet(None) // => "Sorry, who?"
    greet(Some("John")) // => "Hello, John"
    ```
    Using an `Option` with a `None` value is an alternative for `null`, but an alternative in which callers are "forced" to handle the possibility of there being no actual value returned.  This helps to prevent some of the most common bugs, such as the `NullReferenceException`.
- There are two classes of functions, _total_ functions and _partial_ functions.  Total functions are mappings that are defined for every element of the domain.  Partial functions are mappings that are defined for some, but not all, elements of the domain.  Partial functions are problematic as it's not clear what the function should do when given an input for which it cannot compute a result.  The `Option` type offers a perfect solution to model such cases.  One such example is the use of `Option` as a return from a function that tries to convert a `string` to an `int`.  It's partial as not all `string`s can be converted to `int`s, but `Option` allows us to provide a return value from such a function can covers all possible outcomes (i.e. a `Some` in the case the `string` is converted to an `int` and a `None` if not).
- Use "smart constructors" to create objects.  These are similar to factory methods, and implement the necessary logic to ensure the correct type of object is created.  For example, the `Age` class mentioned above could use `Option` within a constructor such as:
    ```
    public static Option<Age> Of(int age) => IsValid(age) ? Some(new Age(age)) : None;
    ```
    This ensures all possible `int` values passed as input return an `Option<Age>`.  Valid ages are encoded as a `Some<Age>` whilst invalid ones are encoded as `None`.  Callers will be given a valid return value, i.e. no chance for a null reference exception, but will be forced to handle both the `Some` and `None` cases.

## Chapter 4 - Designing Function Signatures And Types
- LINQ's `Select` method is more commonly called `Map` in functional programming.  Map is the standard terminology, so you should consider Map and Select synonyms.
- The `Map` function can be expressed as: `(C<T>, (T => R)) => C<R>`.  This means a function that takes some "container" of type `C` containing types of `T` and a function that converts a type `T` to a type `R` will return its results of `R` inside of the same "container" type of `C`.
- Examples of such container types of `C` are `IEnumerable`, `Option`, sets, dictionaries etc.
- The type `C`, a type for which a `Map` function is defined, is known as a Functor.  `IEnumerable` and `Option` are therefore Functors.
- For practical purposes, we can say that anything that has a reasonable implementation of Map is a functor.  A reasonable implementation is one that should apply a function to the container's inner value(s) and, equally importantly, it should do nothing else; that is, Map should have no side effects.
- We can use LINQ's `ForEach` method much like `Map`, however, `ForEach` can have potential side-effects and mutate the data it operates on.  This is because `ForEach` takes an Action rather than a Function to operate on the supplied data, meaning that values are not returned but the data can be directly mutated by the Action.
- Make the scope of the Action that you apply with `ForEach` as small as possible: use `Map` for data transformations and `ForEach` for side effects. This follows the general functional programming idea of avoiding side effects if possible, and isolating them otherwise.
- If we have Option-returning functions, combining those functions could result in returns of an Option of Option, i.e. `Option<Option<int>>`.  This can be problematic to work with as we continually have to "unwrap" each option to get to the inner type inside the option.   This is where the `Bind` function comes in.
- `Bind` takes an Option and an Option-returning function, and applies the function to the inner value of the Option.  The signature of `Bind` is very similar to that of `Map`, but where `Map` takes a "regular" function, `Bind` takes a function that returns an Option.
- The `Bind` function can be expressed as: `(C<T>, (T => C<R>)) => C<R>`.  Where `C` is the container functor, `T` is the underlying input type and `R` is the underlying result type.
- Just as the `Bind` function can "flatten" nested Option types, so too can it flatten nested lists or collections.  The equivalent LINQ method in C# is the `SelectMany` method.
- Types which have a `Bind` function defined on them are known as Monads.   You may often hear the expression "monadic bind" which refers to _the_ `Bind` function allowing the type to be treated as a Monad and not just a function named Bind.
- In addition to the Bind function, monads must also have a `Return` function that "lifts" a normal value `T` into a monadic value `C<T>`.  For the Option type, this is the `Some` function.
- The `Return` function is expressed as: `T => C<T>`.
- For types to be considered "proper" monads, they must adhere to certain "monadic laws".  One of these states that the `Return` function must be quite "dumb" and must do the minimum amount of work required to lift a `T` into a `C<T>` and nothing else.
- We can write code at different levels of abstraction.  We deal with "regular" types and with "elevated" types.  Regular types are defined as `T` and elevated types are defined as `A<T>`.  Elevated types are also referred to as amplified types, or wrapped types.
- These abstractions are constructs that enable us to better work with and represent operations on the underlying types. More technically put, an abstraction is a way to add an "effect" to the underlying type.  An `Option` adds the effect of _optionality_ - not a T, but the possibility of a `T`.  `IEnumerable` adds the effect of _aggregation_ - a sequence of `T`. `Func` adds the effect of _laziness_ - a computation that can be evaluated to obtain a `T`. `Task` adds the effect of _asynchrony_ - a promise that at some point in the future, you'll get a `T`.
- Functions can cross "boundaries" of types.  Some functions are defined as `T => R` - taking a regular type and returning a regular type, whilst some elevate the types, such as `T => C<T>` and others do the reverse, i.e. `C<T> => T`.  The latter types of functions are sometimes referred to as "world-crossing" functions - they take a "regular" type and elevate it into a "container" type (or vice-versa).  Note that often it's not possible to move from an elevated type to a regular type - an `Option<int>` can't always be reduced to an `int` as the Option type may be None.

## Chapter 5 - Designing Programs With Function Composition
- Functional Programming deals a lot with function composition.  This is the ability to "chain" functions together in a single command.
- Functions can only be composed if they have matching types.  The output of the first function must be assignable to the input of the second function.
- In C#, functions are often composed in parentheses in an "outside-in" manner, i.e. `ThirdFunction(SecondFunction(FirstFunction(x)))`.  This is, unfortunately, not great for readability.
- Alternatively, in C#, we can use "method chaining" which involves declaring our functions as static extension methods that work on the type for which we'll execute the function and return a type that can be the input of the next function.  Method chaining allows functions to be expressed more readably in the order that they'll be executed, i.e. `FirstFunction().SecondFunction().ThirdFunction()`
- Function composition is so important that it should apply equally in the world of elevated types. If we have an `Option<Person>`, we should be able to "map" FirstFunction and SecondFunction to it.
- One of the functor laws is that we should be able to apply these functions either together, or one after the other and get the same result. i.e. `var result = opt.Map(FirstFunction).Map(SecondFunction)` should have the same result as `composedFuncs = SecondFunction(FirstFunction(opt));  var result = opt.Map(composedFuncs)`
- You can write entire programs using function composition.  Each function takes its input, processes it, and the output becomes the input for the next function.  You should think of your programs in terms of data flowing through a pipeline of functions.
- There are a number of properties of a function that determine its amenity to composability:
    - Purity - If the function has side-effects, it's less reusable.
    - Chainable - A `this` argument makes it possible to compose through chaining.
    - General - The specific a function, the fewer cases there will be where it's useful.
    - Shape-preserving - The function preserves the "shape" of the structure of its input.  That is, if it takes an `IEnumerable` it returns an `IEnumerable` etc.
- Functions are naturally more composable that `Action`s.  Actions have no return value, so are a "dead-end" for data flow and can only come at the end of the pipeline.
- We can use function composition to implement workflows.  Given a workflow of booking something only if the request is valid, we may implement this imperatively with code such as: `if(validator.IsValid(order)) Book(order);`.  By leveraging the `Option` type and using `Some` to represent no only the existence of data, but of _valid_ data and `None` to represent no valid data, we can compose the equivalent in functions: `Some(order).Where(validator.IsValid).ForEach(Book);`.  Note that the `Book` function is never called if the `IsValid` function results in no valid data.
- The above is an example of programming with statements versus expressions.  Expression have a value, whilst statements don't.  Expressions can have side-effects but often don't while statements only have side-effects so they don't compose.  In C#, if you're using braces, it's a statement.  Programming with expressions helps to promote better program design.  The above is also an example of more declarative programming rather than imperative.

## Chapter 6 - Functional Error Handling
- Error handling in imperative programs usually relies on statements such as `throw` and `try/catch` which produce side-effects and disrupt the normal program flow. Functional Programming strives to minimize side-effects and exceptions are generally avoided.  Errors are captured and returned as part of the _payload_ of data.
- Use `Either` to represent the result of an operation with two different possible outcomes, typically success or failure. An `Either` can be in one of two states:
    - `Left` indicates failure and contains error information for an unsuccessful operation.
    - `Right` indicates success and contains the result of a successful operation.
- Interact with `Either` using the equivalents of the core functions already seen with `Option`:
    - `Map` and `Bind` apply the mapped/bound function _if_ the `Either` is in the `Right` state; otherwise they just pass along the `Left` value.
    - `Match` works similarly to how it does with `Option`, allowing you to handle the `Right` and `Left` cases differently.
    - `Where` is not readily applicable, so `Bind` should be used in its stead for filtering, while providing a suitable `Left` value.
- `Either` is particularly useful for combining several validation functions with `Bind`, or, more generally, for combining several operations, each of which can fail.
- Because `Either` is rather abstract, and because of the syntactic overhead of its two generic arguments, in practice it's better to use a particularized version of `Either`, such as `Validation` and `Exceptional` (both are included in the LaYumba Functional library).
- When working with functors and monads, prefer using functions that stay within the abstraction, like `Map` and `Bind`. Use the downward-crossing `Match` function as little or as late as possible.

## Chapter 7 - Structuring An Application With Functions
- Partial Application is the ability to supply the arguments to a function in a piecemeal manner.  It allows for function to be created in a more generic way, some of the argument are then supplied to the function (partially applied) yielding a new function with those arguments closed out.  The function is then a more specialized version of the more general function.
- Currying is the ability to have a function that takes many arguments and, with the application of each argument, yield a function that takes the single next argument until all arguments are supplied.
- Partial application - You give a function fewer arguments than the function expects, obtaining a function that's particularized with the values of the arguments given so far.  Currying - You don't give any arguments; you just transform an n-ary function into a unary function, to which arguments can be successively given to eventually get the same result as the original function.
- The order of arguments matters: you give the leftmost argument first, so that a function should declare its arguments from general to specific.
- When working with multi-argument functions in C#, method resolution can be problematic and lead to syntactic overhead. This can be overcome by relying on `Func`'s rather than on methods.
- You can inject the dependencies required by your functions by declaring them as arguments. This allows you to compose your application entirely of functions, without compromising on the separation of concerns, decoupling, and testability.

## Chapter 8 - Working Effectively With Multi-Argument Functions
- Summary of core functional patterns, their functions and signatures:  

    | Pattern     | Required Functions | Signature                     |
    |-------------|--------------------|-------------------------------|
    | Functor     | Map                | `F<T> => (T => R) => F<R>`    |
    | Applicative | Return             | `T => A<T>`                   |
    |             | Apply              | `A<T => R> => A<T> => A<R>`   |
    | Monad       | Return             | `T => M<T>`                   |
    |             | Bind               | `M<T> => (T => M<R>) => M<R>` |

- A monad is a type, `M`, for which the following functions are defined:
    - Return: which takes a regular value of type `T` and lifts it into a monadic value of type `M<T>`
    - Bind: which takes a monadic value, `m`, and a world-crossing function, `f`, and "extracts" from `m` its inner value `t` and applies `f` to it
- The monad laws state that a monad should have:
    - Right Identity: meaning that `m == m.Bind(Return)` should be true.  That is, the call to `Bind` unwraps the value inside `m` and the binding of the `Return` function immediately lifts it back up, so the net result is the same as we started with.
    - Left Identity: meaning that `Return(t).Bind(f) == f(t)` should be true.  This is, if you first use `Return` to lift a `t` and then Bind a function, `f`, over the result, that should be equivalent to applying `f` to `t`.
    - Associativity: this is the property that allows operators to be applied to their operands in an arbitrary order.  For addition of numbers we can say that `(a + b) + c == a + (b + c)`.  For the `Bind` function we can say that `m.Bind(f).Bind(g) == m.Bind(x => f(x).Bind(g))`.
- `Apply` and `Bind` are very similar in their functionality, however, the monadic flow we get from using `Bind` has short-circuiting behaviours for several monads - if we're chaining computations, as might be done when performing validation, we would only get the first validation failure.  The applicative functionality provided by `Apply` allows for the independent computations to be combined and the results aggregated.
- The `Apply` function can be used to perform function application in an elevated world, such as the world of `Option`.
- Multi-argument functions can be lifted into an elevated world with `Return`, and then arguments can be supplied with `Apply`.
- Types for which `Apply` can be defined are called applicatives. Applicatives are more powerful than functors, but less powerful than monads.
- Because monads are more powerful, you can also use nested calls to `Bind` to perform function application in an elevated world.
- LINQ provides a lightweight syntax for working with monads that reads better than nesting calls to `Bind`.
- In C#, for any monad, you can use the LINQ query syntax by providing implementations for Select (which is the same as Map) and SelectMany (which is the same as Bind).

## Chapter 9 - Thinking About Data Functionally
- Shared mutable state implies a loss of purity.  If you represent change in the world by mutating objects in your system, you lose the benefits of function purity.  Shared state can also lead to issues such as a lack of thread safety and coupling.
- Local state mutation is ok. This is mutation of variables within the scope of a single function.  Such a function is still considered pure as there's no observable side-effect from outside of the function, however, use of such variable can usually be replaced with built-in LINQ functions such as `Sum`, `Aggregate` etc.
- Most reference types in the .NET framework are mutable, but some are immutable.  Some of the most popular are: `DateTime`, `TimeSpan`, `Delegate`, `Guid`, `String`, `Tuple<T>`, `Uri`.
- In functional programming, things that don't change are represented with immutable objects.  Things that do change are also represented with immutable objects, but changing an object's state actually creates a new instance of the object.
- It's difficult to enforce immutability in C#.  We can get most of the way there, but since techniques like reflection allow mutating state even for private fields, we can never have true immutability.
- When creating immutable objects in C#, ensure that collections are immutable also.  Don't expose a collection via a property and allow consumers to add, remove and modify items within the list.  Keep the actual list private, use an immutable collection to expose to consumers and expose appropriate methods to allow consumers to add, remove and modify the list (internally creating a new list with the desired changes).

## Chapter 10 - Event Sourcing - A Functional Approach To Persistence
- Thinking functionally about data also encompasses storage. Instead of mutating stored data, consider the database as a big immutable collection: you can append new data, but never overwrite existing data.
- Whenever we develop an application with a CRUD approach - that is, updating stored data in-place - we're essentially using the database as a big blob of global mutable state.
- There are two main approaches to immutable storage:
    - Event-based - The database is an ever-growing collection of events.
    - Assertion-based - The database is an ever-growing collection of facts.
- Event sourcing means persisting event data as events occur. The state of an entity need not be stored, because it can always be computed as the "sum" of all events that affected the entity.
- An event-sourced system naturally separates the concerns of reading and writing data, enabling a CQRS architecture that separates between:
    - The command side, where commands are received, validated, and turned into events that are persisted and published.
    - The query side, where events are combined to create view models, which are served to clients and, optionally, cached for better performance.
- Event-sourced systems have several main components:
    - Commands - Simple, immutable data objects encapsulating a request from a client program.
    - Events - Simple, immutable data objects capturing what happened.
    - States - Data objects representing the state of an entity at a certain point in time.
    - State transitions - Functions that take a state and an event, and produce a new state.
    - View models - Data objects for populating views. They're computed from events.
    - Event handlers - These subscribe to events to perform business logic (on the command side) or to update view models (on the query side).
- It's difficult, given two states, to figure out what event may have caused a state transition, but it's easy to figure out the new state, given an event and the previous state.

## Chapter 11 - Lazy Computations, Continuations, And The Beauty Of Monadic Composition
- If you have a function that randomly picks one of two values and is called thusly: `Pick(1 + 2, 3 + 4)`, each of the values is computed as they're bound to the function even though only one value is actually required in the end.  To make the value computation _lazy_, we can wrap each value in functions (the signature of the method would need to change to accept functions too) meaning that the values are not computed unless actually required: `Pick(() => 1 + 2, () => 3 + 4)`.  All that's required to make the evaluation of an expression lazy is, instead of providing an expression, providing a function that will evaluate to that expression. Instead of a `T`, provide a `Func<T>`.
- In general, whenever a function may not use some of its arguments, those arguments should be specified as lazy computations.
- Beware of nesting higher-order functions.  If we have many functions that accept a function as an argument and effectively wrap the invocation of that function in some other behaviour (i.e. writing some logging/tracing before and after the function call), then applying many such functions can make the calling code look very ugly:
    ```csharp
    public void Log(LogMessage message)
    => Instrumentation.Trace("CreateLog"
        , () => ConnectionHelper.Connect(connString
            , c => c.Execute("sp_create_log"
                , message, commandType: CommandType.StoredProcedure)));
    ```
    This is commonly known as the "Pyramid of doom".
- Laziness means deferring a computation until its result is needed. It's especially useful when the result may not be required in the end.
- Lazy computations can be composed to create more complex computations that can then be triggered as needed.
- When dealing with an exception-based API, you can use the Try delegate type.  The Run function safely executes the code in the Try and returns the result wrapped in an Exceptional.
- Higher-Order Functions in the form `(T => R) => R` (that is, functions that take a callback or continuation) can also be composed monadically, enabling you to use flat LINQ expressions rather than deeply nested callbacks.

## Chapter 12 - Stateful Programs And Stateful Computations
- In order to handle state functionally - that is, without state mutation - state must be made available to functions as an input argument, and functions that affect the state must return the updated state as part of their result.
- Stateful computations are functions that take a state (as well as, potentially, other arguments), and return a new state (along with, potentially, a return value). They're also called state transitions.  They have the following signature: `S => (T, S)`.
- Stateful computations can be composed monadically, to reduce the syntactic burden of passing the state from one computation to the next.

## Chapter 13 - Working With Asynchronous Computations
- `Task<T>` represents a computation that will asynchronously deliver a T.
- `Task`'s should be used whenever the underlying operation may have significant latency, such as most I/O operations.
- `Task`-returning functions can be composed with `Map`, `Bind`, and several other combinators to specify error handling or multiple retries.
- If `Task`'s are independent, they can be run in parallel. You can use Task as an applicative, and providing several Task s with Apply runs them in parallel.
- If you have two monads, `A` and `B`, you may like to stack them up in values like `A<B<T>>`, to combine the effects of each monad.
- Traverse can be used to invert the order of monads in the stack.
- Implementing the query pattern for such a stack allows you to combine `A`'s, `B`'s, and `A<B<>>`'s with relative ease.
- Still, stacked monads tend to be cumbersome, so use them sparingly.

## Chapter 14 - Data Streams And The Reactive Extensions
- The `IObservable` interface provides an abstraction to represent event streams.  If you think of an array as a sequence of values in space (space in memory, that is),
then you can think of `IObservable` as a sequence of values in time.
- With an `IEnumerable`, you can enumerate its values at your leisure.  All values are produced synchronously.  With an `IObservable`, you can observe the values as they come.  `IObservable` is like a `Task<T>` that produces multiple values instead of a single value.
- The `IObservable` contract can produce three messages. `OnNext` is raised when a new value is produced.  `OnCompleted` is raised when no more values will be produced.  `OnError` is raised in the event of an error.  `OnCompleted` and `OnError` signal the end of the production of values, once either of these events are raised, no more values will be produced by the `IObservable`.
- Observables work in tandem with Observers.  Observables produce values, observers consume them.
- You can convert other types to `IObservable`. `Observable.Return` converts a single `T` to an observable.  `.ToAsync` converts a `Task<T>`, and .`ToObservable` converts an `IEnumerable<T>`.
- Writing a program with `IObservable`'s involves three steps:
    - Create `IObservable`'s using the methods in `System.Reactive.Linq.Observable`.
    - Transform and combine `IObservable`'s using the operators in Rx, or other operators you may define.
    - Subscribe to and consume the values produced by the `IObservable`.
    - Associate an observer to an `IObservable` with `Subscribe`.
    - Remove an observer by disposing of the subscription returned by `Subscribe`.
    - Separate side effects (in observers) from logic (in stream transformations).
- When deciding on whether to use `IObservable`, consider the following:
    - `IObservable` allows you to specify logic that spans multiple events.
    - `IObservable` is good for modelling unidirectional data flows, not request/response.

## Chapter 15 - An introduction To Message-Passing Concurrency
- Shared mutable state that is accessed concurrently can cause difficult problems:
    - For this reason, it's best to avoid shared mutable state entirely, and this can often be achieved in parallel processing.
    - In other scenarios, notably in multithreaded applications that need to model real-world entities, shared mutable state is often required.
    - Access to shared mutable state must be serialized to avoid inconsistent changes to the data. This can be achieved using locks, but also using lock-free techniques.
- Message-passing concurrency is a technique that avoids locks by restricting state mutation to processes (actors/agents) that have exclusive ownership of some state, which they can access single-threadedly in reaction to messages they're sent.
- An actor/agent is a lightweight process featuring:
    - An inbox, in which messages sent to it are queued up.
    - Some state, of which it has exclusive ownership.
    - A processing loop, in which it processes messages sequentially, taking actions such as creating and communicating with other agents, changing its state, and performing side effects.
- Agents and actors are fundamentally similar, but there are important differences:
    - Actors are distributed, whereas agents are local to a single process.
    - Unlike with agents, the actor model includes a model for error handling with supervisor actors that can take action if the supervised actor fails, resulting in very robust systems.
- Message-passing concurrency feels quite different from other functional programming techniques, mainly because functional programming works by composing functions, whereas actors/agents tend to work in a fire-and-forget fashion.
- It's possible to write high-level functional API's with agent-based or actor-based implementations.

