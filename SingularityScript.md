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
