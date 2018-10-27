# annotate_ifdef
## What's it?
Ever wonder which ifdef matches which endif and how those ifdef/endif pairs nest each other?
If you have an advanced IDE, that won't be a problem. But in many cases, we only have text editor with basic syntax highlight.
`annotate_ifdef` is a utility to help understand the ifdef/endif hierarchy.

`annotate_ifdef` reads file content, adds annotation to line heads, and prints lines to standard output. At the end, it reports whether all `ifdef` are closed by `endif` and whether there are redundant `endif`.

## Command line
Two command line arguments are expected.

`annotate_ifdef <language> <filename>`

`language` should be one of C/makepp/Verilog. It's case insensitive.

## Example
Assume `example.h` has the content as follows.
```
#ifdef A
#define B 5
#if C==2
#define D
#endif
#endif
```
Run command `annotate_ifdef c example.h`. The output is like this.
```
$ annotate_ifdef c example.h
Checking example.h c.
r       1       :#ifdef A
|       2       :#define B 5
|r      3       :#if C==2
||      4       :#define D
|L      5       :#endif
L       6       :#endif
        7       :
PASS
```
