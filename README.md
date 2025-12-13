# Umni's Fennel Fork

[Fennel][1] is a lisp that compiles to Lua. It has macros and zero runtime overhead.
This is my fork of it on top of which I've put various patches for random things.

## Installation
1. clone this repo
2. run `make` (you need to have `lua` installed)
3. use `fennel` outside of CC or `fennel.lua` inside of CC (the only difference is the #! at the start of the file)

## List of patches
- The compiler and repl now work inside CC:Tweaked (use `fennel.lua` inside CC)
- The `include` special no longer uses `package.preload` for its bundling and instead uses a local table to achieve the same thing more cleanly
- `&while` in all of the looping forms (it's just a negated `&until`)
- made more functions available to macros:
  - `compile` - takes an ast and returns lua code as a string
  - `load` - lua 5.2+; takes lua code as a string and returns a function that executes it when called
- alias macros: a macro that is a quoted symbols or list instead of a function is now legal and every occurrence of it will be replaced with the corresponding value (without the need to call it)
- macros returning macros: if a macro returns a function then that function will be treated as another macro and immediately expanded as well
- more macros: the following macros have been added:
  - `<<-` - identical to `->>` except that the arguments are iterated in reverse order


[1]: https://git.sr.ht/~technomancy/fennel
