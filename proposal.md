# Proposal for Ferropt

Like in Rust, Ferropt shall also allow Structs, Functions, Variables, but in a different sense.

A Program can be:
- Function-like: each Program Entity is a function, always return a value with a type defined in runtime, after execution; might contain directly passed parameters
- Script-like: no data to be *returned*, but possibly states like successful/failed (like `Ok`/`Err`); "parameters" are always supplied by environments or (global/helper) functions

## Basics

There is no definite visibility in a Program: anything in a Program can be access anywhere in a Program.

All defined Declarations must use a symbol prefix before their names, preventing conflicts with keywords

Most types shall be the same as defined in Rust, but there are no macros and modules.

Immutable variable declaration: `let $name = expr`

Mutable variable declaration: `let* $name = expr`

Function declaration: `fn #name(...) -> type {...}`

Struct declaration: `struct #name`, `struct #name(...)` (tuple), `struct #name {...}`

Struct field declaration: `$name: type`

Trait declaration: `trait #name : type {...}`

There is also lifetime management in Ferropt.

References: `::name` is equilavent to `#name`, `#::path` for absolute path

Naming conventions are likely the same as in Rust.

### Libraries

By the runtime itself, there are no built-in *standard* functions or utilities, but likely only primitives and operators without supplementary functions.

The project itself may provide some standard utilities as separate crates that are fundamental in programming.

## Binary

Interpreted Binaries with Bytecodes from Sources are formatted and defined as below.

Header consists of
- magic number (12 bytes): 0x89 `FERROPT` 0x00 `BTS`
- format version:
  - major version (2 bytes): `u16`
  - minor version (2 bytes): `u16`
- list of version specific headers:
  - length (2 bytes): `u16`
- vendor string (UTF-8; maximally 255 characters)
- list of vendor specific headers:
  - length (2 bytes): `u16`
Content consists of
- import table
- bytecodes
