# C# Guidelines
> [!NOTE]
> We have chosen to pronounce C# as "C Hashtag".

## Language naming conventions
Conventions for identifier names are used throughout the .NET projects. These conventions provide consistency for names, but the compiler doesn't enforce them.

By convention, C# programs use `PascalCase` for type names, namespaces, and all public members. In addition, the team uses the following conventions:

- Interface names start with a capital `I`.
- Attribute types end with the word `Attribute`.
- Enum types use a singular noun for nonflags, and a plural noun for flags.
- Identifiers shouldn't contain two consecutive underscore (`_`) characters. Those names are reserved for compiler-generated identifiers.
- Use meaningful and descriptive names for variables, methods, and classes.
- Prefer clarity over brevity.
- Use PascalCase for class names and method names.
- Use camelCase for method arguments, local variables, and private fields.
- Use PascalCase for constant names, both fields and local constants.
- Private instance fields start with an underscore (`_`).
- Static fields start with `s_`.
- Avoid using abbreviations or acronyms in names, except for widely known and accepted abbreviations.
- Use meaningful and descriptive namespaces that follow the reverse domain name notation.
- Choose assembly names that represent the primary purpose of the assembly.
- Avoid using single-letter names, except for simple loop counters. Also, syntax examples that describe the syntax of C# constructs often use the following single-letter names that match the convention used in the C# language specification. Syntax examples are an exception to the rule.

  - Use `S` for structs, `C` for classes.
  - Use `M` for methods.
  - Use `v` for variables, `p` for parameters.
  - Use `r` for `ref` parameters.

### Pascal case

Use pascal casing ("PascalCasing") when naming a `class`, `interface`, `struct`, or `delegate` type.

```csharp
public class DataService
{
}
```

```csharp
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```

```csharp
public struct ValueCoordinate
{
}
```

```csharp
public delegate void DelegateType(string message);
```

When naming an `interface`, use pascal casing in addition to prefixing the name with an `I`. This prefix clearly indicates to consumers that it's an `interface`.

```csharp
public interface IWorkerQueue
{
}
```

When naming `public` members of types, such as fields, properties, events, use pascal casing. Also, use pascal casing for all methods and local functions.

```csharp
public class ExampleEvents
{
    // A public field, these should be used sparingly
    public bool IsValid;

    // An init-only property
    public IWorkerQueue WorkerQueue { get; init; }

    // An event
    public event Action EventProcessing;

    // Method
    public void StartEventProcessing()
    {
        // Local function
        static int CountQueueItems() => WorkerQueue.Count;
        // ...
    }
}
```

When writing positional records, use pascal casing for parameters as they're the public properties of the record.

```csharp
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```

### Camel case

Use camel casing ("camelCasing") when naming `private` or `internal` fields and prefix them with `_`. Use camel casing when naming local variables, including instances of a delegate type.

```csharp
public class DataService
{
    private IWorkerQueue _workerQueue;
}
```

When working with `static` fields that are `private` or `internal`, use the `s_` prefix and for thread static use `t_`.

```csharp
public class DataService
{
    private static IWorkerQueue s_workerQueue;

    [ThreadStatic]
    private static TimeSpan t_timeSpan;
}
```

When writing method parameters, use camel casing.

```csharp
public T SomeMethod<T>(int someNumber, bool isValid)
{
}
```

## General Conventions
Our common code conventions derive from those recommended by Microsoft. These expand the default conventions configured in Visual Studio and for our projects.

### String data

- Use `string interpolation` to concatenate short strings, as shown in the following code.

    ```cs
    string displayName = $"{nameList[n].LastName}, {nameList[n].FirstName}";
    ```

- To append strings in loops, especially when you're working with large amounts of text, use a [StringBuilder](https://learn.microsoft.com/en-us/dotnet/api/system.text.stringbuilder) object.

    ```cs
    var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
    var manyPhrases = new StringBuilder();
    for (var i = 0; i < 10000; i++)
    {
        manyPhrases.Append(phrase);
    }
    //Console.WriteLine("tra" + manyPhrases);
    ```

### Arrays

- Use the concise syntax when you initialize arrays on the declaration line. In the following example, you can't use `var` instead of `string[]`.

    ```cs
    string[] vowels1 = { "a", "e", "i", "o", "u" };
    ```

- If you use explicit instantiation, you can use `var`.

    ```cs
    var vowels2 = new string[] { "a", "e", "i", "o", "u" };
    ```

### `try-catch` and `using` statements in exception handling

- Use a [try-catch](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/exception-handling-statements#the-try-catch-statement) statement for most exception handling.

    ```cs
    static double ComputeDistance(double x1, double y1, double x2, double y2)
    {
        try
        {
            return Math.Sqrt((x1 - x2) * (x1 - x2) + (y1 - y2) * (y1 - y2));
        }
        catch (System.ArithmeticException ex)
        {
            Console.WriteLine($"Arithmetic overflow or underflow: {ex}");
            throw;
        }
    }
    ```

- Simplify your code by using the C# [using statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/using). If you have a `try-finally` statement in which the only code in the `finally` block is a call to the `Dispose` method, use a `using` statement instead.

  In the following example, the `try-finally` statement only calls `Dispose` in the `finally` block.

    ```cs
    Font bodyStyle = new Font("Arial", 10.0f);
    try
    {
        byte charset = bodyStyle.GdiCharSet;
    }
    finally
    {
        if (bodyStyle != null)
        {
            ((IDisposable)bodyStyle).Dispose();
        }
    }
    ```

  You can do the same thing with a `using` statement.

    ```cs
    using (Font arial = new Font("Arial", 10.0f))
    {
        byte charset2 = arial.GdiCharSet;
    }
    ```

  Use the new [`using` syntax](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/using) that doesn't require braces:

    ```cs
    using Font normalStyle = new Font("Arial", 10.0f);
    byte charset3 = normalStyle.GdiCharSet;
    ```

### `new` operator

- Use one of the concise forms of object instantiation, as shown in the following declarations.

    ```cs
    var firstExample = new ExampleClass();
    ```

  ```csharp
  ExampleClass instance2 = new();
  ```

  The preceding declarations are equivalent to the following declaration.

    ```cs
    ExampleClass secondExample = new ExampleClass();
    ```

- Use object initializers to simplify object creation, as shown in the following example.

    ```cs
    var thirdExample = new ExampleClass { Name = "Desktop", ID = 37414,
    Location = "Redmond", Age = 2.3 };
    ```

  The following example sets the same properties as the preceding example but doesn't use initializers.

    ```cs
    var fourthExample = new ExampleClass();
    fourthExample.Name = "Desktop";
    fourthExample.ID = 37414;
    fourthExample.Location = "Redmond";
    fourthExample.Age = 2.3;
    ```

### Event handling

- Use a lambda expression to define an event handler that you don't need to remove later:

```cs
public Form2()
{
    this.Click += (s, e) =>
        {
            MessageBox.Show(
                ((MouseEventArgs)e).Location.ToString());
        };
}
```

The lambda expression shortens the following traditional definition.

```cs
public Form1()
{
    this.Click += new EventHandler(Form1_Click);
}

void Form1_Click(object? sender, EventArgs e)
{
    MessageBox.Show(((MouseEventArgs)e).Location.ToString());
}
```

### Static members

Call `static` members by using the class name: *ClassName.StaticMember*. This practice makes code more readable by making static access clear.  Don't qualify a static member defined in a base class with the name of a derived class.  While that code compiles, the code readability is misleading, and the code may break in the future if you add a static member with the same name to the derived class.

### Implicitly typed local variables

- Use [implicit typing](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables) for local variables when the type of the variable is obvious from the right side of the assignment.

    ```cs
    var message = "This is clearly a string.";
    var currentTemperature = 27;
    ```

- Don't use `var` when the type isn't apparent from the right side of the assignment. Don't assume the type is clear from a method name. A variable type is considered clear if it's a `new` operator, an explicit cast or assignment to a literal value.

    ```cs
    int numberOfIterations = Convert.ToInt32(Console.ReadLine());
    int currentMaximum = ExampleClass.ResultSoFar();
    ```

- Don't use variable names to specify the type of the variable. It might not be correct. Instead, use the type to specify the type, and use the variable name to indicate the semantic information of the variable. The following example should use `string` for the type and something like `iterations` to indicate the meaning of the information read from the console.

    ```cs
    var inputInt = Console.ReadLine();
    Console.WriteLine(inputInt);
    ```

- Avoid the use of `var` in place of [dynamic](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types). Use `dynamic` when you want run-time type inference. For more information, see [Using type dynamic (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/interop/using-type-dynamic).

- Use implicit typing for the loop variable in `for` loops.

  The following example uses implicit typing in a `for` statement.

    ```cs
    var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
    var manyPhrases = new StringBuilder();
    for (var i = 0; i < 10000; i++)
    {
        manyPhrases.Append(phrase);
    }
    //Console.WriteLine("tra" + manyPhrases);
    ```

- Don't use implicit typing to determine the type of the loop variable in `foreach` loops. In most cases, the type of elements in the collection isn't immediately obvious. The collection's name shouldn't be solely relied upon for inferring the type of its elements.

  The following example uses explicit typing in a `foreach` statement.

    ```cs
    foreach (char ch in laugh)
    {
        if (ch == 'h')
            Console.Write("H");
        else
            Console.Write(ch);
    }
    Console.WriteLine();
    ```

### Place the using directives outside the namespace declaration

When a `using` directive is outside a namespace declaration, that imported namespace is its fully qualified name. The fully qualified name is clearer. When the `using` directive is inside the namespace, it could be either relative to that namespace, or its fully qualified name.

```csharp
using Azure;

namespace CoolStuff.AwesomeFeature
{
    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
```

Assuming there's a reference (direct, or indirect) to the `WaitUntil`> class.

Now, let's change it slightly:

```csharp
namespace CoolStuff.AwesomeFeature
{
    using Azure;

    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
```

And it compiles today. And tomorrow. But then sometime next week the preceding (untouched) code fails with two errors:

```console
- error CS0246: The type or namespace name 'WaitUntil' could not be found (are you missing a using directive or an assembly reference?)
- error CS0103: The name 'WaitUntil' does not exist in the current context
```

One of the dependencies has introduced this class in a namespace then ends with `.Azure`:

```csharp
namespace CoolStuff.Azure
{
    public class SecretsManagement
    {
        public string FetchFromKeyVault(string vaultId, string secretId) { return null; }
    }
}
```

A `using` directive placed inside a namespace is context-sensitive and complicates name resolution. In this example, it's the first namespace that it finds.

- `CoolStuff.AwesomeFeature.Azure`
- `CoolStuff.Azure`
- `Azure`

Adding a new namespace that matches either `CoolStuff.Azure` or `CoolStuff.AwesomeFeature.Azure` would match before the global `Azure` namespace. You could resolve it by adding the `global::` modifier to the `using` declaration. However, it's easier to place `using` declarations outside the namespace instead.

```csharp
namespace CoolStuff.AwesomeFeature
{
    using global::Azure;

    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
```

## Style guidelines

In general, use the following format for code samples:

- Use four spaces for indentation. Don't use tabs.
- Align code consistently to improve readability.
- Limit lines to 65 characters to enhance code readability on docs, especially on mobile screens.
- Break long statements into multiple lines to improve clarity.
- Use the "Allman" style for braces: open and closing brace its own new line. Braces line up with current indentation level.
- Line breaks should occur before binary operators, if necessary.

### Comment style

- Use single-line comments (`//`) for brief explanations.
- Avoid multi-line comments (`/* */`) for longer explanations. Comments aren't localized. Instead, longer explanations are in the companion article.
- For describing methods, classes, fields, and all public members use [XML comments](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/).
- Place the comment on a separate line, not at the end of a line of code.
- Begin comment text with an uppercase letter.
- End comment text with a period.
- Insert one space between the comment delimiter (`//`) and the comment text, as shown in the following example.

    ```cs
    // The following declaration creates a query. It does not run
    // the query.
    ```

### Layout conventions

Good layout uses formatting to emphasize the structure of your code and to make the code easier to read. Microsoft examples and samples conform to the following conventions:

- Use the default Code Editor settings from Visual Studio (smart indenting, four-character indents, tabs saved as spaces).
- Write only one statement per line.
- Write only one declaration per line.
- If continuation lines aren't indented automatically, indent them one tab stop (four spaces).
- Add at least one blank line between method definitions and property definitions.
- Use parentheses to make clauses in an expression apparent, as shown in the following code.

    ```cs
    if ((startX > endX) && (startX > previousX))
    {
        // Take appropriate action.
    }
    ```
