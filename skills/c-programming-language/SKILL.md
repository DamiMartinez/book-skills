---
name: c-programming-language
description: Applies Kernighan & Ritchie's "The C Programming Language" (2nd Edition, ANSI C) framework — pointer/array duality and pointer arithmetic, reading declarations by the right-left rule, manual memory management and ownership, undefined behavior, the preprocessor and separate compilation, storage classes/linkage, and C's "trust the programmer" minimalism — to writing, reviewing, or debugging C code. Use whenever the user wants a "K&R approach," mentions "pointer arithmetic," "declaration reflects use," "malloc/free," "undefined behavior," "storage class," "header guards," or is writing/debugging C, tracking down a segfault, buffer overflow, or memory leak, or asking how a gnarly C declaration should be read — even if they don't name the book.
---

# The C Programming Language (K&R, 2nd Edition)

Apply this skill when writing, reviewing, or debugging C code, or explaining C semantics — grounded in K&R's philosophy that C trusts the programmer completely: no hidden costs, no runtime safety net, and correctness is the programmer's explicit responsibility at every step.

## Core concepts

**"Trust the programmer"** — C deliberately omits bounds checking, garbage collection, and most runtime safety nets, on the premise the programmer knows what they're doing and wants no hidden cost. This means C code that "looks fine" can still be wrong in ways the compiler won't catch — when reviewing C, actively look for what the language *won't* stop, not just syntax errors.

**Pointer/array duality & pointer arithmetic** — `a[i]` is defined as `*(a + i)`; arrays decay to pointers in most expressions, and pointer arithmetic is scaled by the pointee's size automatically. Understanding this equivalence is the key to reading and writing idiomatic C (pointer-walking a buffer instead of indexing, passing arrays as pointer+length). When debugging array/pointer code, mentally rewrite between the two forms to spot off-by-one or scaling errors.

**Declarations mirror use (the right-left / "spiral" rule)** — A declaration like `int *a[10]` or `int (*a)[10]` should be read by working outward from the identifier following C's precedence rules (`[]` and `()` bind tighter than `*`), not left-to-right. When a declaration is confusing (arrays of pointers, pointers to functions, pointers to arrays), decompose it this way rather than guessing — this is the single most common source of "wait, what does this even declare" confusion in C.

**Manual memory management & ownership** — Every `malloc`/`calloc` needs an unambiguous owner responsible for exactly one matching `free`; there's no garbage collector to fall back on. When reviewing allocation code, explicitly trace: who allocates, who's responsible for freeing, and what happens on every exit path (including error returns) — leaks and double-frees are almost always a broken answer to "who owns this."

**Undefined behavior** — Many operations (signed integer overflow, out-of-bounds access, use of uninitialized values, dereferencing freed/null pointers, strict-aliasing violations) are left *undefined*, not just implementation-defined, meaning the compiler is free to assume they never happen and can optimize accordingly — code that "seems to work" can still be wrong and break under a different compiler or optimization level. Never write code that depends on a specific behavior in an undefined case; flag suspected UB explicitly rather than reasoning about what "probably happens."

**The preprocessor & separate compilation** — Macros are pure textual substitution (parenthesize macro arguments and the whole expansion to avoid precedence bugs); header files declare interfaces shared across translation units, and should use include guards to survive multiple inclusion. Keep implementation in `.c` files and only the interface in `.h` files — a bloated header is usually a sign the module's interface isn't actually minimal.

**Storage classes & linkage** — `static` at file scope limits a function/variable's linkage to that translation unit (use it by default for anything not part of a module's public interface); `extern` shares a symbol across files; `auto` (default, rarely written) is stack-allocated and local. When reviewing multi-file C, check that internal helpers are `static` and that nothing has broader visibility than it needs.

**Manual strings & buffers** — C strings are just null-terminated char arrays; the standard library (`strcpy`, `strcat`, `sprintf`, etc.) does no bounds checking, so buffer size and null-termination are entirely the programmer's job. When reviewing string/buffer handling, check every write path for the actual allocated size versus what's being written, and prefer bounded variants (`strncpy`, `snprintf`) with explicit size tracking.

**Structs, unions, and direct memory layout** — Structs/unions/bit-fields give direct control over memory layout, which is powerful for systems programming (binary protocols, hardware registers) but means padding, alignment, and endianness are real, visible concerns — not abstracted away.

**Minimalism in style** — K&R's own code style favors small functions, terse but meaningful names, and avoiding unnecessary abstraction — the language gives you just enough to build what you need and no more. Apply this as a style preference when writing new C: prefer the plain, direct construct over a clever or over-engineered one.

## How to apply this

1. **When writing or reviewing C**, actively hunt for what the compiler *won't* catch: unchecked bounds, unowned allocations, UB-dependent logic, uninitialized reads — the risks the language leaves entirely to the programmer.
2. **For pointer/array bugs**, rewrite the expression between array and pointer form to spot scaling/off-by-one errors.
3. **For a confusing declaration**, decompose it via the right-left rule rather than guessing what it means.
4. **For any `malloc`**, trace ownership explicitly — who frees it, and does every exit path (including errors) still free it exactly once?
5. **For anything that "seems to work but feels fragile,"** ask whether it secretly relies on undefined or implementation-defined behavior, and flag it even if it currently compiles fine.
6. **For multi-file code**, check header hygiene (include guards, minimal public interface) and that internal symbols are `static`.
7. **For string/buffer code**, verify the actual buffer size against every write, and prefer bounded standard-library variants.

Keep feedback concrete and tied to the actual code — this is a lens for catching the specific class of bugs C's minimalism makes possible, not a style lecture.
