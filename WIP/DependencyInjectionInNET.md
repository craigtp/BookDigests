# Book Digest: Dependency Injection In .NET

Title     : Dependency Injection In .NET  
Author(s) : Mark Seemann  
ISBN-10   : 1935182501  
ISBN-13   : 978-1935182504

## Chapter 1 - Putting Dependency Injection On The Map
- DI is nothing more than a collection of design principles and patterns. It's more about a way of thinking and designing code than it is about tools and techniques.
- Dependency Injection is known as many different things:  Dependency Injection (DI), Inversion Of Control, Third-Party Connect and others.
- Dependency Injection is a technique of programming that is a means to an end, it is not a goal of itself.  It's primary purpose is to enable loose coupling within your applications and ensure that your applications remain maintainable over time.
- In order to be able to apply DI and achieve loose coupling, programs must be written in such a way that you program to an interface, not an implementation. 
- There are many myths around the purpose of DI - that it is only relevant for late binding, unit testing, being an abstract factory or that it requires a DI container library.  None of these are true.  Whilst DI does help with late binding, unit testing etc. it is not only relevant to those ends.
- DI helps with Late Binding, which means that a concrete implementation of a class can be changed at runtime without requiring code changes or recompilation.
- DI helps with extensibility.  Because dependencies are always interfaces, we can wrap one concrete implementation of an interface with another concrete implementation (similar but not the same as inheritance) and pass the "wrapped" implementation to the consumer.  This is the "decorator" design pattern.
- DI helps with maintainability. Because dependencies are always interfaces, we can program to the interface only ensuring loose coupling.  Loose coupling makes code extensible, and extensibility makes it maintainable.  Also, as classes are broken down, the responsibility of each class becomes clearly defined and constrained, maintenance of the overall application becomes easier. This is a known benefit of the Single Responsibility Principle, which states that each class should have only a single responsibility.
- DI helps with Testability. Because dependencies are always interfaces, we can more easily provide a "mock" or "test double" for a classes dependencies, allowing testing of the class in isolation of the dependencies which it is normally requires.
- DI helps break down the "composition" of your application by introducing "Seams".  Everywhere we decide to program against an interface instead of a concrete type, we introduce a Seam into the application. A Seam is a place where an application is assembled from its constituent parts.
- Dependencies can be stable or volatile.  Stable dependencies, such as programming against the .NET framework's base classes themselves do not necessarily need to be injected. A DI Container itself, will likely be a stable dependency. Volatile Dependencies are the focal point of DI. It's for Volatile Dependencies that we introduce Seams into our application.
- Stable dependencies are those that: are always available, highly unlikely to change, new versions won't contain breaking changes and the implementations contain deterministic algorithms.
- Volatile dependencies are those that:  introduce a requirement to setup and configure a runtime environment for the application (i.e. a database), possibly does not yet exist (still in development), isn't available on all machines in all environments, contains non-deterministic behaviour (i.e. System.DateTime.Now or System.Random)
- Object Composition, Interception and Object Lifetime Management are the three dimensions of DI.  We can compose applications while intercepting dependencies and controlling their lifetimes.
- Object Composition is the providing of all of the dependencies to a "chain" of classes.  The top-level class is the "composition root".
- Object lifetime means that the lifetime of the dependency is not controlled by the consumer, but by the code that provides the dependency.  This may or may not be a DI Container.
- Interception is the ability to "wrap" or "decorate" a concrete dependency with additional functionality (by wrapping in another class that implements and consumes the same interface) and is an application of the GoF Decorator design pattern.
- In order to be truly effective, DI must be pervasive throughout your codebase.

## Chapter 2 - A Comprehensive Example
- 