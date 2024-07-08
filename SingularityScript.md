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

### Rich text

This was chosen after a very careful consideration of how functional usage of whitespace to separate tokens has led to profound wars on how to deal with multi-word identifiers. `PascalCase`, `camelCase`, `snake_case`, `kebab-case` - all this insanity and wasted effort and mental resources. By storing the source code in a [rich text](https://en.wikipedia.org/wiki/Formatted_text) format, we finally solve this nonsense and allow developers to have human understandable identifiers in their programs.

Plus, such format will also allow us to carefully store metadata (such as language revision) to empower tooling even further. For example, a source file written in the old revision can be automatically converted to a newer revision upon opening it.

Also, using rich text will send the message that careful highlighting of the source text is expected. Old-style editors like vi[m] and Emacs are inhuman messes that we don't want to deal with. Then, there should be a standard for sharing themes. Different people have different preferences on how their code should be highlighted and having a common standard will encourage cooperation and sharing of highlighting themes.

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
