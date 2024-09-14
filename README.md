# Fully-associative-mapping


---

# Fully Associative Mapping - Cache Simulation in C



## Table of Contents
- [About the Project](#about-the-project)
- [Features](#features)
- [Directory Structure](#directory-structure)
- [How to Run](#how-to-run)
- [Input Data Format](#input-data-format)
- [Cache Algorithms](#cache-algorithms)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About the Project

This project simulates a **write-through** or **write-back** direct-mapped cache in C. The simulation analyzes cache performance by computing:
- Cache hits
- Cache misses
- Main memory reads and writes

The project is structured to accept different trace files that simulate memory operations, showcasing cache efficiency in terms of read and write policies. For more detailed information about the project and cache algorithms, refer to the [Project Documentation](./docs/pa3.pdf).

---

## Features

- **Write-through & Write-back Support**: Choose between two popular cache write policies.
- **Cache Hit/Miss Analysis**: Tracks and reports the number of cache hits and misses.
- **Main Memory Operations**: Monitors and reports the number of memory reads and writes.
- **Trace File Input**: Simulates cache behavior with user-provided trace files.

---

## Directory Structure

```
Fully-associative-mapping/
├── bin/                   # Compiled binary files
├── docs/                  # Project documentation
│   └── pa3.pdf
├── src/                   # Source code
│   ├── sim.c
│   └── sim.h
├── traces/                # Sample trace files
│   ├── trace0.txt
│   ├── trace1.txt
│   ├── trace2.txt
│   └── trace3.txt
├── Makefile               # Build instructions
├── LICENSE                # License for the project
├── README.md              # Project README
└── testplan.txt           # Test plan for the cache simulator
```

---

## How to Run

### Requirements

- GCC compiler or any C compiler.
- Make utility.

### Build the Project

To compile the project, navigate to the root directory and run:

```bash
make
```

This will create an executable `sim` in the `bin/` directory.

### Example Usage

The program accepts two arguments: the **write policy** (either `wt` for write-through or `wb` for write-back) and the **trace file** that contains memory operations.

Example commands:

```bash
./bin/sim wt traces/trace0.txt  # Write-through policy
./bin/sim wb traces/trace3.txt  # Write-back policy
```

The output will display the number of cache hits, misses, reads, and writes.

---

## Input Data Format

The program reads a trace file where each line represents a memory operation. These files simulate memory accesses and consist of:
- **Hexadecimal addresses** for memory locations.
- **Operation types**: Read or Write operations.

Example of a trace file (`trace0.txt`):

```
R 0x1A2B3C4D
W 0x5E6F7A8B
R 0x0C0D0E0F
#eof
```

---

## Cache Algorithms

### Read Algorithm
1. Validate inputs.
2. Convert the hexadecimal address to a parsable binary format.
3. Extract the **tag** and **index** from the formatted binary string.
4. Check the cache block corresponding to the index.
5. If the tag matches and the block is valid:
   - Increment cache hits.
6. Otherwise, mark a cache miss and increment main memory reads.
7. Handle dirty blocks in the case of a write-back policy.
8. Set the block as valid and store the tag.

### Write Algorithm
1. Validate inputs.
2. Convert the hexadecimal address to a parsable binary format.
3. Extract the **tag** and **index**.
4. Check the cache block:
   - If a match is found, mark the block as dirty (for write-back).
   - Increment cache hits.
5. Otherwise, handle cache misses and update the block.

---

## Results

The program outputs statistics such as:
- **Cache hits**: Number of successful cache accesses.
- **Cache misses**: Number of accesses that resulted in memory reads.
- **Main memory reads**: Number of times data was read from memory.
- **Main memory writes**: Number of times data was written to memory.

The results are presented in the terminal and can also be saved to a file by redirecting the output.

Example:
```bash
./bin/sim wt traces/trace0.txt > results.txt
```

---

## Contributing

If you'd like to contribute to the project, please follow these steps:
1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request explaining your changes.

We welcome contributions in the form of feature requests, bug reports, or performance improvements.

---

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.

---

