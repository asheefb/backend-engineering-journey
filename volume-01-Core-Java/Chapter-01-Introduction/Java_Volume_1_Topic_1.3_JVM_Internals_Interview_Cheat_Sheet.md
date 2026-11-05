# JVM Internals --- Interview Cheat Sheet

## Java Volume 1 · Topic 1.3

Use this for quick revision. Refer to the detailed notes for
explanations and diagrams.

## 1. JVM in 30 seconds

-   JVM is a software runtime that loads and executes Java bytecode.
-   `javac`: `.java` → `.class`.
-   JVM executes bytecode; source is not required at runtime.
-   Bytecode is portable across compatible JVMs; JVM implementations are
    platform-specific.
-   Compatibility depends on class-file version and runtime APIs.

## 2. JVM Architecture

``` text
JVM
├── Class Loader Subsystem
├── Runtime Data Areas
├── Execution Engine (Interpreter / JIT / GC)
└── JNI + Native Method Libraries
```

## 3. Runtime Data Areas

  Area                  Short answer
  --------------------- --------------------------------------------------
  Heap                  Shared; objects and arrays; GC-managed
  Java Stack            Per thread; method frames, locals, operand stack
  Method Area           Conceptual class-level structures/metadata
  PC Register           Per thread; current JVM instruction
  Native Method Stack   Supports native method execution

**HotSpot nuance:** class metadata is stored in Metaspace (native
memory). Do not claim all static data is physically stored in one
universal Method Area.

### Stack vs Heap

``` text
Stack: local reference emp  ---------> Heap: Employee object
```

-   Object/array: conceptually heap; local reference: stack frame.
-   Multiple references can point to one object.
-   Method call pushes a frame; return pops it (LIFO).
-   Deep recursion can cause `StackOverflowError`.
-   Circular references can be collected if unreachable from GC roots.
-   `obj = null` does not immediately delete the object.
-   Local variables must be definitely assigned; instance fields receive
    defaults.

## 4. Class Loaders

``` text
Bootstrap
   ↑ parent
Platform
   ↑ parent
Application
```

-   Bootstrap: core classes (`String`, `Object`, `System`).
-   Platform: other platform classes; Java 9+ Platform loader replaced
    Extension loader.
-   Application: application classes and dependencies.
-   Parent delegation: ask parent first; child tries if parent cannot
    load.
-   Module system and class-loader system are distinct.

## 5. Class Lifecycle

``` text
Loading -> Linking -> Initialization
             |
             +-- Verification
             +-- Preparation
             +-- Resolution
```

-   Loading: locate/read class and create runtime representation.
-   Verification: validate class-file and bytecode constraints/type
    safety.
-   Preparation: allocate static fields and assign default values.
-   Resolution: symbolic references become direct references as needed.
-   Initialization: execute explicit static initializers and static
    blocks.

**Remember:** `static int count = 10;` gets default `0` during
preparation, then explicit `10` during initialization.

## 6. Interpreter vs JIT

  -----------------------------------------------------------------------
  Interpreter                         JIT
  ----------------------------------- -----------------------------------
  Executes bytecode                   Compiles hot code into native code

  Allows execution to begin           Can improve repeated/hot code
                                      performance

  Doesn't compile every method first  Uses runtime profiling/heuristics
  -----------------------------------------------------------------------

-   Not every method is JIT-compiled.
-   JIT does not overwrite `.class` on disk.
-   JVM may deoptimize or recompile.

## 7. Garbage Collection

-   GC reclaims heap objects no longer reachable from GC roots.
-   Eligible for collection ≠ collected immediately.
-   `System.gc()` is a request/hint, not a guarantee.
-   GC uses reachability, not simple reference counting.

  -----------------------------------------------------------------------
  Algorithm               Core idea               Trade-off
  ----------------------- ----------------------- -----------------------
  Mark & Sweep            Mark reachable; reclaim Can leave fragmentation
                          dead                    

  Mark & Compact          Mark, reclaim, move     Compaction work
                          survivors together      

  Copying                 Copy live objects to    Needs destination space
                          another space           
  -----------------------------------------------------------------------

## 8. Generational GC

**Generational hypothesis:** most objects die young; fewer survive
long-term.

``` text
Young Generation: Eden | S0 | S1
Old Generation
```

-   Eden: new objects typically allocated here in traditional
    generational collectors.
-   S0/S1: alternate as From/To survivor spaces.
-   Live objects are copied; unreachable objects are reclaimed.
-   Survivor spaces reduce fragmentation and help track object age.
-   Objects surviving enough collections may be promoted to Old
    Generation.
-   Promotion may also depend on size, space and collector policy.
-   Not every modern collector uses this exact layout.

## 9. Minor vs Major vs Full GC

  Term               Common usage
  ------------------ ---------------------------------------------
  Minor / Young GC   Focused on Young Generation
  Major GC           Commonly Old Generation; terminology varies
  Full GC            Generally involves the entire heap

**Interview caution:** Major GC is not necessarily Full GC. Exact
terminology and behavior vary by collector/tool.

## 10. Common interview questions

**1. What is JVM?**\
Runtime that loads and executes Java bytecode.

**2. Why is Java platform-independent?**\
Compatible bytecode can run on different platforms with compatible JVMs.

**3. Does JVM execute `.java` directly?**\
Normally no; `javac` compiles source into bytecode.

**4. Heap vs Stack?**\
Heap is shared and holds objects/arrays; each thread has its own stack
of method frames.

**5. What happens on a method call?**\
A frame is pushed; it is popped when the method returns.

**6. What is parent delegation?**\
A class loader asks its parent before trying to load a class itself.

**7. What are linking stages?**\
Verification, preparation and resolution.

**8. What happens during preparation?**\
Static fields receive default values.

**9. Why verify bytecode?**\
Class files may come from other compilers or be generated/modified; JVM
validates bytecode constraints.

**10. Interpreter vs JIT?**\
Interpreter executes bytecode; JIT compiles hot code to native code.

**11. When is an object eligible for GC?**\
When no path from GC roots can reach it.

**12. Can circular references be collected?**\
Yes, if the cycle is unreachable from all GC roots.

**13. Does `System.gc()` force immediate GC?**\
No; it is only a request/hint.

**14. Why generational GC?**\
Most objects die young, so the young area can be collected more
frequently.

**15. Where are new objects allocated in a traditional generational
collector?**\
Typically Eden.

**16. Why two Survivor spaces?**\
They alternate as From/To spaces so live objects can be copied and the
source space reclaimed.

**17. What is promotion?**\
Moving a surviving young object to Old Generation according to collector
policies.

**18. Minor vs Major vs Full GC?**\
Commonly Young collection, Old collection, and whole-heap collection
respectively; terminology varies.

## 11. Avoid these incorrect claims

-   Every JVM stores static fields in the same physical memory area.
-   Every object must physically reside on the heap in every optimized
    execution.
-   GC immediately deletes an object when its last reference disappears.
-   `System.gc()` guarantees collection.
-   Every Major GC is a Full GC.
-   Every collector uses Eden + S0 + S1.
-   Promotion depends only on a fixed age threshold.

## 12. Still to cover

-   Java 17 GC choices and collector-specific behavior.
-   Practical `System.gc()` behavior.
-   GC logs, heap dumps and analysis.
-   `jcmd`, `jmap`, `jstat`, VisualVM, Java Flight Recorder.
-   `StackOverflowError`, `OutOfMemoryError`, memory leaks.
-   Final Topic 1.3 assessment.