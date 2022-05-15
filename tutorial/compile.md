# Compiling Emergent
Follow these steps to compile your Emergent program:
1. Goto the directory with the `emergent` binary
2. Compile with  `./emergent <source.emg>'
3. If successful, you should have produced a `<source.cpp>` file
4. Compile the `source.cpp` file
5. Perform `./source.cpp <input.txt> <model> <t> <output.txt>` to execute the code

## Notes:
- Perform `./emergent --help` for all options for the Emergent compiler
- The `input.txt` and `output.txt` will keep the same dimensions
- `<t>` is the amount of timesteps to execute
- `<model>` is the specific CA model you are executing with

## Other Tutorials
- [Installing Emergent](install.md)
- [Coding your first Automaton](walkthrough.md)
