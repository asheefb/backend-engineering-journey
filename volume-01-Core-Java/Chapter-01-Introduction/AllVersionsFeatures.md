# Java Versions and Their Features (Java 1 to Java 27)

If you are preparing for Java developer interviews, especially Java Backend Developer roles, you should understand the important features introduced in each Java version.

The most important versions to focus on are Java 8, 11, 17, 21 and 25.

As of November 2026, Java 27 is the latest feature release, while Java 25 is an LTS release.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.oracle.com\&sz=32)

Releases+1

## 1. Java version timeline

| Version  | Release year | LTS |
| -------- | ------------ | --- |
| Java 1.0 | 1996         | No  |
| Java 5   | 2004         | No  |
| Java 6   | 2006         | No  |
| Java 7   | 2011         | No  |
| Java 8   | 2014         | Yes |
| Java 9   | 2017         | No  |
| Java 10  | 2018         | No  |
| Java 11  | 2018         | Yes |
| Java 12  | 2019         | No  |
| Java 13  | 2019         | No  |
| Java 14  | 2020         | No  |
| Java 15  | 2020         | No  |
| Java 16  | 2021         | No  |
| Java 17  | 2021         | Yes |
| Java 18  | 2022         | No  |
| Java 19  | 2022         | No  |
| Java 20  | 2023         | No  |
| Java 21  | 2023         | Yes |
| Java 22  | 2024         | No  |
| Java 23  | 2024         | No  |
| Java 24  | 2025         | No  |
| Java 25  | 2025         | Yes |
| Java 26  | 2026         | No  |
| Java 27  | 2026         | No  |

## 2. Important Java versions and features

### Java 5 – Generics and language improvements

- Generics
- Enhanced for loop
- Autoboxing and unboxing
- Enum
- Annotations
- Varargs

### Java 7 – Language improvements

- String in switch statements
- Try-with-resources
- Diamond operator (`<>`)
- Multi-catch exceptions
- Binary literals
- Underscores in numeric literals

### Java 8 – Most important for interviews

Must learn

- Lambda Expressions
- Functional Interfaces
- Stream API
- Method References
- Default and Static Methods in Interfaces
- Optional Class
- New Date and Time API (`java.time`)
- Collectors
- forEach()
- Nashorn JavaScript Engine

Example:

```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::println);
```

### Java 9 – Modular programming

- Java Platform Module System (JPMS)
- JShell
- Factory methods for collections (`List.of()`, `Set.of()`, `Map.of()`)
- Private methods in interfaces
- Stream API improvements
- Optional improvements

### Java 10 – Local variable type inference

- `var` keyword
- Local variable type inference
- Application Class-Data Sharing improvements

Example:

```
var name = "Asheef";
var age = 25;
```

### Java 11 – Important for backend development

Must learn

- Standard HTTP Client API
- New String methods (`isBlank()`, `lines()`, `strip()`, `repeat()`)
- `var` in lambda parameters
- New Files methods (`readString()`, `writeString()`)
- Single-file source-code execution

Example:

```
String name = " Java ";

System.out.println(name.strip());
System.out.println(name.isBlank());
System.out.println(name.repeat(2));
```

### Java 12

- Switch Expressions (preview)
- String API improvements
- Compact Number Formatting

### Java 13

- Text Blocks (preview)
- Switch Expressions improvements

Example:

```
String message = """
        Hello
        Welcome to Java
        """;
```

### Java 14

- Switch Expressions (standard)
- Records (preview)
- Pattern Matching for `instanceof` (preview)
- Helpful NullPointerExceptions

Example:

```
int result = switch (day) {
    case 1 -> 100;
    case 2 -> 200;
    default -> 0;
};
```

### Java 15

- Text Blocks (standard)
- Sealed Classes (preview)
- Hidden Classes
- Records (second preview)

### Java 16

- Records (standard)
- Pattern Matching for `instanceof` (standard)
- Stream.toList()
- Sealed Classes (second preview)

Example:

```
record Employee(int id, String name) {}

Employee emp = new Employee(101, "Asheef");

System.out.println(emp.name());
```

### Java 17 – Important for modern Java development

Must learn

- Sealed Classes (standard)
- Pattern Matching for `instanceof` (standard)
- Strong encapsulation of JDK internals
- Switch Pattern Matching (preview)
- Enhanced Pseudo-Random Number Generators

Example:

```
public sealed class Animal
    permits Dog, Cat {
}

final class Dog extends Animal {
}

final class Cat extends Animal {
}
```

### Java 21 – Major modern Java release

Must learn

- Virtual Threads
- Pattern Matching for switch (standard)
- Record Patterns
- Sequenced Collections
- String Templates (preview in Java 21)
- Structured Concurrency (preview)
- Unnamed Patterns and Variables

Example:

```
Thread.startVirtualThread(() -> {
    System.out.println("Running virtual thread");
});
```

### Java 25 – Latest LTS release

- Compact Source Files and Instance Main Methods
- Module Import Declarations
- Flexible Constructor Bodies
- Scoped Values
- Compact Object Headers
- Ahead-of-Time Method Profiling
- Primitive Types in Patterns (preview)

Java 25 became generally available on September 16, 2025.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://blogs.oracle.com\&sz=32)

java+1



## 3. Java 18–27: Other important releases

| Version | Important features                                                                                  |
| ------- | --------------------------------------------------------------------------------------------------- |
| Java 18 | UTF-8 by default, Simple Web Server, Code Snippets in JavaDoc                                       |
| Java 19 | Virtual Threads (preview), Record Patterns (preview), Pattern Matching for switch (preview)         |
| Java 20 | Virtual Threads improvements, Record Patterns improvements, Scoped Values (incubator)               |
| Java 22 | Foreign Function & Memory API, Unnamed Variables and Patterns, Stream Gatherers (preview)           |
| Java 23 | Markdown Documentation Comments, Module Import Declarations (preview), Primitive Patterns (preview) |
| Java 24 | Stream Gatherers (standard), Class-File API (preview), Structured Concurrency improvements          |
| Java 26 | HTTP/3 support in HTTP Client API, improvements to garbage collection and runtime                   |
| Java 27 | Latest feature release; consult release notes for its finalized feature set                         |

Reference: [Official JDK Release Notes](https://www.oracle.com/java/technologies/javase/jdk-relnotes-index.html?utm_source=chatgpt.com).

## 4. What should you learn for Java interviews?

For a Java Backend Developer role, I recommend this priority:

| Priority | Java version | Topics                                            |
| -------- | ------------ | ------------------------------------------------- |
| 1        | Java 8       | Lambda, Streams, Optional, Functional Interfaces  |
| 2        | Java 11      | String APIs, HTTP Client, Files                   |
| 3        | Java 17      | Records, Sealed Classes, Pattern Matching         |
| 4        | Java 21      | Virtual Threads, Switch Patterns, Record Patterns |
| 5        | Java 25      | Modern language improvements                      |

## 5. Recommended learning checklist

Java version preparation

0/18 completed

Java 8 – Lambda Expressions

Java 8 – Functional Interfaces

Java 8 – Stream API

Java 8 – Method References

Java 8 – Optional

Java 8 – Date and Time API

Java 9 – Modules and Collection Factory Methods

Java 10 – var keyword

Java 11 – String API improvements

Java 11 – HTTP Client

Java 14 – Switch Expressions

Java 16 – Records

Java 17 – Sealed Classes

Java 17 – Pattern Matching

Java 21 – Virtual Threads

Java 21 – Record Patterns

Java 21 – Pattern Matching for switch

Java 25 – Modern Java features

Reset progress

My recommendation: Don't try to memorize every Java version. Master Java 8 thoroughly first, then Java 11, 17 and 21. These will give you a strong foundation for modern Java backend interviews.