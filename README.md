# blc-mb

Binary Lambda Calculus evaluation engine written in Malbolge. Features:
- Garbage collection
- Monadic I/O
- Tail call optimisation
- Compatible with existing BLC8 programs

## Usage

Steps:
- Navigate to the folder blc-vX.XX with the desired version.
- If you have bzip3 installed, you can download the .bz3 archive as it's much smaller. If not, then download the other ones.
- Unpack it.
- Built fast20.c with clang. For most machines, `clang -O3 -march=native -mtune=native fast20.c -o f20` will do.

Example programs:
- `( cat examples/hilbert.Blc ; echo -n "123" ) | ./f20 blc.mb`
- `( cat examples/reverse.Blc ; echo -n 'Hello, world!' ) | ./f20 blc.mb`
- `echo "*Hello" | ./f20 blc.mb`

## Issues you might stumble upon

- If fast20 segfaults, then you most probably haven't pointed it towards a valid program to execute.
- The interpreter might take a while to "warm up". For me, it seems to take around 30 seconds before starting to parse.
- Parsing is pretty slow, expect the Hilbert curve program to take around 2 hours.
- If you don't have a Linux machine, you're out of luck because fast20 doesn't work on Windows. PRs welcome!

There are a few error codes. The interpreter will not signal exhausting heap memory and will invoke undefined behavior.

- `E00` - Unexpected EOF
- `E01` - Memory exhausted.
- `E02` - Unfinished expression.
- `E03` - Referencing an undefined variable.
- `E04` - Continuations exhausted.
- `E05` - Malformed term.
