# makefile

This is a makefile I have been using for a while in a variety of projects,
intended to be drop-and-use so that minimal maintenance is needed in the
makefile itself, as long as I keep consistent directory and file naming
schemes.  It works mainly for C and C++ with partial support for Fortran
sources as well.

## What does it do?

Coupled with `makedepend.py`, this `makefile` attempts to automatically setup
linking dependencies (which `.o` files are necessary for linking a certain
program?) without ever having to manually modify the makefile itself.  Note
that header dependencies (which `.h` files are necessary to compile a given
`.c` file?) are not dealt with directly and instead are taken care of by
GCC's `-MMD -MP -MF` flags.

## How to make it work?

In order for the setup to work, a couple of conventions must be followed.

- Name source files containing `main()` function or `PROGRAM` subroutine
  as `main_name.*`, which will generate binary files `bin/name`
- Put all header files (`.h`, `.hpp`, `.inc`, ...) in `include/` directory
- Put all source files (`.c`, `.cpp`, ...) in `src/` directory
- For Fortran only, `name_*.f` are set as dependencies of `bin/name`

## How do I use it?

Make targets include:

- **cleanbuild**  delete all temporary files (`*.o`, `*.mod`)
- **clean**       cleanbuild + delete binary programs (`bin/*`)
- **cleanall**    clean + delete dependency information (`.d/`)
- **[default]**   when called without target, builds every `main_name.*`
