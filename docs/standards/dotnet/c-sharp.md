!!! info "This documentation supports and overrides Resharper's default C# conventions."

!!! summary "C# conventions - order of priority."
    There are various sources of authority for C# conventions, but they should be followed in the following order:

    1. This documentation
    2. [Resharper]'s recommmendations
    3. Microsoft's [Conventions][MS Conventions] and [Guidelines][MS Guidelines]

## Types

??? fail "Don't use arrays."
    Unless you have an exceptional reason.

    [Justification](https://blogs.msdn.microsoft.com/ericlippert/2008/09/22/arrays-considered-somewhat-harmful/)

    The .NET Framework provides a whole host of optimised collection types; pick the one that's right for you.

    C# is a high level language; we shouldn't pre-emptively optimise on memory usage by managing fixed-size collections ourselves - 90% of the time the Framework knows best.

    - **Parameters** and **Return values** should almost always return an **interface**, not a concrete type
        - Use `ICollection<>`, `IEnumerable<>`, `IDictionary<>`, `IQueryable<>` etc.
        - Don't use an array `<>[]`, and don't use `List<>` or another concrete implementation in the method signature.
    - **Public properties** should usually be **interface** types, not concrete implementations
        - especially if they are properties guaranteed by an **interface**
    - Almost all collection variables in implementation code should be a .NET class type, not an array
        - Use `List<>`, `Dictionary<>`, `HashTable<>`, `Stack<>`, `Queue<>` etc.
        - Don't use an array `<>[]`

    If you absolutely want a fixed size collection because it **makes your code clearer** or **less prone to error** and it doesn't matter that it's a **value type** not a **reference type**, you may use an array.

    However, that sort of thing is usually only appropriate for high performance bare metal applications, or other low level code such as hardware emulators, drivers etc.

    That sort of code is not usually written in C#, and is almost never necessary in a web application.

## Usings

??? success "Use top-level usings, not namespaced identifiers."

    ```csharp
    //Bad
    System.Nullable<int> number;

    //Better
    using System;
    ...
    Nullable<int> number;

    //Best
    int? number;
    ```

    You should only have to provide namespaces in your actual code if you are clarifying an ambiguous reference:
        
    ```csharp
    using System;
    using Unity.Engine;

    System.Random dotNetRandomNumberGenerator;
    Unity.Engine.Random unityRandomNumberGenerator;
    ```

## Identifiers

??? fail "Don't put redundant information in identifiers such as variable or method names."
    - No Hungarian notation (the IDE tells you types!)
    - some type names are common and this is acceptable, but be sensible:

    ```csharp
    var person = new Person(); //Fine

    var personClass = new Person(); //Bad

    var personList = new List<Person>(); //Bad

    var people = new List<Person>(); //Good
    ```

## Variable Initialisation

??? fail "Don't bother assigning the default initial value to a variable."
    ```csharp
    //Redundant
    bool myBool = false;
    string myString = null;
    MyObject myObject = null;
    int myInt = 0;
    ```

??? success "Do initialise collections, or object types before attempting to use their members."
    ```csharp
    //Necessary
    var myList = new List<T>();
    var myObject = new MyObject();
    ```

??? fail "Don't use Constructor initialisation unless you need to run logic or accept parameters."
    ```csharp
    public class MyClass
    {
        //Bad
        private bool _isAwesome;

        public MyClass()
        {
            _isAwesome = true;
        }

        ...

        //Good
        private bool _isAwesome = true;
        //No default constructor needed!

        ...

        //Fine
        private bool _isAwesome

        public MyClass(bool isAwesome)
        {
            _isAwesome = isAwesome;
        }

        //In C#6 and newer, you can do this for properties as well!
        public bool IsAwesome { get; set; } = true;
        //No default constructor needed!
    }
    ```

    As before, don't bother setting members to their type's default values.

## Method declaration

??? success "Use expression body syntax."
    From C#6, if the whole of your method is a single expression (a one line statement), you can use a shorter syntax.

    This is incredibly common in read service layers that simply call on a repository.

    ```csharp
    //Pre C#6
    public IEnumerable<Thing> GetAllTheThings()
    {
        return _thingRepo.List();
    }

    //C#6 and newer
    public IEnumerable<Thing> GetAllTheThings() =>
        _thingRepo.List();
    ```
??? success "Only use async in the naming suffix when there is no corresponding synchronous method"
    - this keeps method names simpler
    - your IDE will tell you how to use the method anyway
    
    ```csharp
    public async Task<IEnumerable<Thingy>> GetAsync()
    {
        return await _thingRepo.List();
    }
    
    public IENumerable<Thingy> Get()
    {
        return _otherThingRepo.List();
    }
    ```

[Resharper]: https://www.jetbrains.com/resharper/
[MS Conventions]: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions
[MS Guidelines]: https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/
