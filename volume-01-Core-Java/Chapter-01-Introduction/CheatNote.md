* James Gosling and his team at Sun Microsystems created Java with the idea Write Once, Run Anywhere (WORA)

### UnsupportedClassVersionError
when we try to run different compiled version .class in different java version 
    Ex: When you compile using Java 17:
          --- 
  *     javac Test.java
  By default, Java 17 generates class files with major version 61.
  
   Java 8 supports class files up to major version 52.

  - ### How can we make it work?

      Compile the source using Java 17 but target Java 8 compatibility:

        javac --release 8 Test.java

    This generates Java 8-compatible bytecode and restricts the available Java APIs to those provided by Java 8.

    Now Java 8 can execute it.
  - | Java version | Class-file major version |
    | ------------ | -----------------------: |
    | Java 8       |                       52 |
    | Java 11      |                       55 |
    | Java 17      |                       61 |
    | Java 21      |                       65 |
    | Java 25      |                       69 |

  - | Bytecode compiled with | Java 8 JVM | Java 17 JVM | Java 21 JVM |
    | ---------------------- | ---------- | ----------- | ----------- |
    | Java 8                 | ✅          | ✅           | ✅           |
    | Java 17                | ❌          | ✅           | ✅           |
    | Java 21                | ❌          | ❌           | ✅           |
  - ❌ - Need to User --release
