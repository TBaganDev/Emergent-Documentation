# Installing Emergent
Follow these steps to install Emergent:
1. Install the C++ v17 Compiler specific to your platform, see comprehensive list [here](https://www.stroustrup.com/compilers.html).
2. Compile the `ast.cpp` to `ast.o`
3. Compile the `codegen.cpp` to `codegen.o`
4. Compile the `lexer.cpp` to `lexer.o`
5. Compile the `parser.cpp` to `parser.o`
6. Compile the `main.cpp` with dependencies `ast.o` `codegen.o` `lexer.o` `parser.o` to `emergent`


### Other Tutorials
- [Compiling Emergent](compile.md)
- [Coding your first Automaton](compile.md)
