# SingularityScript

A programming language designed to help humans achieve technological singularity.

## Design principles

### The most important design principle - human is the weakest link in the system

Every aspect of the language should help the developer and empower the developer. There is no place for arrogance here. The whole language (**and tooling!**) should act as a ramp to help a new person learn it.

### Don't cling to the code you've written yourself - it will be refactored by automatic refactoring tools in the future

*“Water is fluid, soft, and yielding. But water will wear away rock, which is rigid and cannot yield. As a rule, whatever is fluid, soft, and yielding will overcome whatever is rigid and hard. This is another paradox: what is soft is strong.” – [Lao Tzu](https://en.wikipedia.org/wiki/Laozi)*

Sure, it makes us feel proud to see machines bending to the will of our code. So much so that we try to preserve those lines of code as long as possible. But for what purpose if not only greed? The world is constantly changing, moving on. You cling to the past and suddenly you're no longer relevant.

This also implied that the language should have a very clear unambiguous grammar so writing parser and automatic refactoring tools can be done with minimum effort.

### The language should be similar to the plain English language

Yes, there are some elementary grade school math notation that is universal, such as `a = b + c` and `f(x, y)` but we shouldn't assume much more and we shouldn't create more cryptic notation that will confuse readers and learners.

This also means that keywords should be full words. `function`, not `func` or `fn`.

### The language itself should be as fluid as possible

The main paradigm should be [generic programming](https://en.wikipedia.org/wiki/Generic_programming) with [concepts](https://en.wikipedia.org/wiki/Concept_(generic_programming)) being the main tool to design libraries of highly generic and reusable code. Classical [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming) uses rigid class hierarchies. Concepts and [type erasure](https://en.wikipedia.org/wiki/Type_erasure) can achieve the same things and more.

### Metadata-based

Old languages were mostly concerned into translation into the assemly language and, ultimately, into the machine code. Hence the emphasis on low-level stuff such as number of bits in the integer types used. But such design misses the elephant in the room - actual problems we're trying to solve.

Plus, once the code started to get big, languages introduced hacks to introduce new names for types such as C's [typedef](https://en.cppreference.com/w/cpp/language/typedef) and C++'s [using](https://en.cppreference.com/w/cpp/language/type_alias). However, they do not introduce new concrete types so one can write nonsensical code such as:

```
using temperature = float;
using humidity = float;

temperature human_healthy_temperature = 36.6f;

set_humidity(human_healthy_temperature);
```

And it will compile, run and produce nonsense. So the new language has to use strong types and these types should have only a very strict amount of operations that make actual sense. The actual integer or floating point types used under the hood are implementation details that should be left to expert developers or taken as template parameters.

Take for example a simple formula of motion:

```
new_position = old_position + velocity * duration;
```

Here we have 3 distinct types - absolute position, velocity and duration. But what does `velocity * duration` return? A new type, call it `offset`, `displacement` or whatever. And only certain operations between types makes sense. You move position by the offset but adding positions together doesn't make any sense. So in C++ you'd have 4 different classes with operator overloads between them. And any math that doesn't make sense is a compile error. The logic bugs are caught even before you run a program.

And metadata-based programming solves even classes of vulnerabilities. Take for example an SQL injection? Where rogue user-typed string is interpreted directly and allows attacker to perform arbitrary SQL queries on a server? Well, imagine we had a library that uses `sql_unescaped_string` and `sql_escaped_string` and the only way to get `sql_escaped_string` would be to use library-proven code and `sql_escaped_string` is either immutable or checks for escape/escapes the string manually every time it is modified. And we only execute queries with `sql_escaped_string`. Now any code written with such library is immune to SQL injection because escaping of all of the strings is enforced by the library at the type system level. You can't physically pass an unescaped string, it will not compile. We just solved the whole class of attacks with a sound type system. This is what metadata-based programming is about.

### Rich text

This was chosen after a very careful consideration of how functional usage of whitespace to separate tokens has led to profound wars on how to deal with multi-word identifiers. `PascalCase`, `camelCase`, `snake_case`, `kebab-case` - all this insanity and wasted effort and mental resources. By storing the source code in a [rich text](https://en.wikipedia.org/wiki/Formatted_text) format, we finally solve this nonsense and allow developers to have human understandable identifiers in their programs.

Plus, such format will also allow us to carefully store metadata (such as language revision) to empower tooling even further. For example, a source file written in the old revision can be automatically converted to a newer revision upon opening it.

Also, using rich text will send the message that careful highlighting of the source text is expected. Old-style editors like vi[m] and Emacs are inhuman messes that we don't want to deal with. Then, there should be a standard for sharing themes. Different people have different preferences on how their code should be highlighted and having a common standard will encourage cooperation and sharing of highlighting themes.

### Do Unicode right this time, at last!!!

Most people don't even know the difference between "code point" and "scalar value" and misspell the former as "codepoint". Thankfully, yours truly is a Unicode expert and a language lawyer so we'll finally have the language that can actally handle Unicode in a sane way.

There will be a proper iteration over code units, scalar values and extended grapheme clusters provided by the standard library. There will be a compiler-provided [Unicode Character Database](https://www.unicode.org/ucd/) along with the ability to load a user supplied one during the reflection pass and at run-time. Finally, sane Unicode.

### No sentinel values

[Null was a billion dollar mistake](https://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare/). C++ started slowly fixing it by adding [`std::optional`](https://en.cppreference.com/w/cpp/utility/optional) but the biggest fix is to not introduce such dangerous stuff in the first place.

### Provide safe language constructs and standard library by default and give unsafe escape hatch for the experts

Again, humans are amazing at creating bugs. So any wrong memory access or logic error should be caught as fast as possible. In fact, at this point I am convinced that simple [integer overflow](https://en.wikipedia.org/wiki/Integer_overflow) should crash the program by default. Expert developers will be given expert integers that wrap silently or [saturate](https://en.wikipedia.org/wiki/Saturation_arithmetic) but the average developer can't be expected to know all of this and should be given a very big and explicit error message on overflow.

## Tooling

### Provide detailed progress reports

Old languages wee limited by old tools, most of them written ad hoc without any clear unifying vision. Just people solving immediate problems without thinking big.

Since we're building the language from scratch, it makes perfect sense to write an IPC mechanism to report progress back to the IDE or similar tools. One can easily imagine a live report of the amount of tokens processed, abstract syntax tree built, optimization passes... All of this would be fed back to a nice progress bar in the IDE or a web interface to a CI pipeline.

### Minimize the usage of the command line

Yes, we'll need a full toolchain to be able to run on build servers but it doesn't mean we have to go back to the insane mess of cryptic compiler flags.

The idea is to have every tool invokation be supplied with a configuration file written in standardized format such as [YAML](https://en.wikipedia.org/wiki/YAML) or [TOML](https://en.wikipedia.org/wiki/TOML).

### Any Git (SVN, Mercurial, SMB share) repo is a package you can import into your own project

I mean, why bother inventing a new package format when plain file system combined with methods of sharing files are already invented. Sure, there will need to be a standartized manifest format (like `Cargo.toml` in Rust) but otherwise the most utilitarian approach is to piggyback on other thechnologies that are already invented and proven to work. Plus, as new methods of sharing data are being invented, we add them to the tooling.

Also, binary packages are limited in general. You can't expect a lone open source developer to compile their package for an exotic architecture or an exotic configuration. By going source first we encourage maximum cooperation and sharing of the code.

### The most important part - humane IDE

You can't hook new developers onto your language if you make onboarding process too difficult. So we need an IDE that can create a "Hello world!" project in a few clicks. And maybe upload it on GitHub in a few more clicks. That will show developers how easy it is to use the tools and empower them to learn the language further.

So yeah, there should be a nice full-fledged "New project..." wizard. Then there should be a nice window with the list of project dependencies and another nice wizard helping developers import external packages into their project. There should be source templates for simple things.

The main editing window should leverage [Language Server Protocol](https://en.wikipedia.org/wiki/Language_Server_Protocol) providing developers with all the modern conveniences.

Humans are notorious at making mistakes. Upon failed compilation, there should be a clear list of errors with clicking on them taking the user to the line containing the error and maybe even suggesting a fix. IDE can also do basic syntax checking as the user types and highlight obvious syntax errors with red squigglies just like most editors with spell checking do.

There should be a nice and fancy prgress bar (or even a progress window for developers who want the most insight) during the build process.

Once the project is built, it's all about user-friendly debugging with fancy stuff like conditional breakpoints watching the values of variables in real time, etc.

Once the code is proven to work, the next step is documenting it (or at least the public API) so that other people can understand what it does with as minimum effort as possible. Here there should be an automatic documentation generator which would automatically generate the documentation stubs for the original developer to fill. Plus, once we're at this stage, the IDE itself can monitor for changes in public API and highlight missing documentation.

Once the code is built and documented. There should be a unit testing framework. In fact, in ideal case it should parse the documentation with AI and generate unit tests just from the documentation. Here's where fancy stuff like code coverage also comes in. The IDE can generate nice graphs of how well the code is documented, tested, etc.

Finally, once all the stuff is done, there should be a nice wizard to export the project as a package for other developers to import into their own projects (unless it's an end-user executable, of course).

Of course, with the rise of AI there could be a different workflow. Developer can just engineer prompts for some kind of LLM similar to ChatGPT and have it write the actual code. Yet all the coverage tools would still stay the same.

## Good proof-of-concept libraries to work on

### Generalized [Newtonian physics](https://en.wikipedia.org/wiki/Classical_mechanics) library

As in, the number of dimensions should be arbitrary and the same code could generate 1D, 2D, 3D, 4D physics, etc. And the number type should also be specified by the user of the library, such as [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) `binary32`, [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) `binary64`, [`bfloat16`](https://en.wikipedia.org/wiki/Bfloat16_floating-point_format), [fixed-point](https://en.wikipedia.org/wiki/Fixed-point_arithmetic), [arbitrary-precision](https://en.wikipedia.org/wiki/Arbitrary-precision_arithmetic), etc.

### Generalized [ray tracing](https://en.wikipedia.org/wiki/Ray_tracing_(graphics)) library

Such library would provide abstract primitives for ray tracing which would then be handled by either [software rendering](https://en.wikipedia.org/wiki/Software_rendering), [DirectX Raytracing](https://en.wikipedia.org/wiki/DirectX_Raytracing), [Vulkan](https://en.wikipedia.org/wiki/Vulkan), [OptiX](https://en.wikipedia.org/wiki/OptiX), etc.

The choice can be either compile-time or run-time. In the second case, there could be a system detector for available APIs which would provide a list for the user to select.

Of course, a demo app could be combined with a physics library to provide a nice ray traced physics sandbox to get users hooked on the language.
