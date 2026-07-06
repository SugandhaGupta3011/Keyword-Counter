# Keyword Counter

A high-performance C++ implementation of a **Keyword Counter** using a **Max Fibonacci Heap** and a **hash table** to efficiently maintain and query the most frequently occurring keywords from a continuously updated data stream.

Originally developed in 2019 as part of **COP 5536 – Advanced Data Structures** at the University of Florida, this project demonstrates the implementation of advanced priority queue operations and efficient data structure design for large-scale keyword processing.

---

## Overview

Search engines continuously process millions of keyword updates and frequently need to determine the current **Top N** most popular searches.

This project efficiently supports:

- Inserting new keywords with an initial frequency
- Updating the frequency of existing keywords
- Retrieving the **N** most frequent keywords
- Preserving the data structure after each query by reinserting removed nodes

Instead of repeatedly sorting all keywords, the implementation combines a **Max Fibonacci Heap** with a **hash table**, enabling efficient updates and fast retrieval of the highest-frequency keywords.

---

## Architecture

```text
                 Input File
                     │
                     ▼
          Parse Keyword Operations
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
    Hash Table           Max Fibonacci Heap
(keyword → node)        (frequency ordering)
          │                     │
          └──────────┬──────────┘
                     ▼
          Top N Keyword Queries
                     │
                     ▼
               output_file.txt
```

---

## Features

- Custom implementation of a Max Fibonacci Heap
- Hash table for constant-time keyword lookup
- Efficient frequency updates using Increase Key
- Cascading cuts and heap consolidation
- Supports repeated Top-N queries
- Restores heap state after each query
- Designed to handle datasets containing **over one million keywords**

---

## Data Structures

### Max Fibonacci Heap

Maintains keyword frequencies while supporting efficient priority queue operations.

Implemented operations include:

- Insert
- Remove Maximum
- Increase Key
- Consolidation
- Cascading Cut
- Heap Meld

### Hash Table

Maps each keyword directly to its corresponding Fibonacci Heap node, allowing frequency updates without traversing the heap.

---

## Project Structure

```text
.
├── keywordcounter.cpp
├── Makefile
├── input.txt
├── Report.pdf
├── output_file.txt
└── README.md
```

---

## Build

Compile the project using the provided Makefile:

```bash
make
```

---

## Usage

Run the executable with an input file:

```bash
./keywordcounter input.txt
```

The generated output is written to:

```text
output_file.txt
```

---

## Input Format

The input stream consists of three types of records.

### Insert or Update a Keyword

```text
$keyword frequency
```

Example:

```text
$facebook 5
$youtube 3
$facebook 10
```

If the keyword already exists, its frequency is increased. Otherwise, a new node is inserted into the Fibonacci Heap.

---

### Retrieve the Top N Keywords

```text
N
```

Example:

```text
3
```

Outputs the three most frequently occurring keywords.

---

### Stop Processing

```text
stop
```

Terminates the program.

---

## Example

### Sample Input

```text
$facebook 5
$youtube 3
$facebook 10
$amazon 2
$gmail 4
3
stop
```

### Sample Output

```text
facebook,youtube,gmail
```

---

## Algorithm

1. Read each operation from the input stream.
2. For a new keyword, create a Fibonacci Heap node and insert it into the heap.
3. For an existing keyword, locate its node using the hash table and increase its frequency.
4. Perform cascading cuts if the heap property is violated.
5. For a Top-N query:
   - Remove the maximum node repeatedly.
   - Write the extracted keywords to the output file.
   - Reinsert the removed nodes to restore the heap.

---

## Time Complexity

| Operation | Complexity |
|-----------|------------|
| Insert | O(1) amortized |
| Increase Key | O(1) amortized |
| Hash Table Lookup | O(1) average |
| Remove Maximum | O(log n) amortized |
| Top N Query | O(N log n) amortized |

---

## Assumptions

- Keyword frequencies are positive integers.
- Keywords contain no spaces.
- Keywords may contain alphanumeric or special characters.
- Keyword matching is exact (e.g., `#youtube` and `#youtube_music` are treated as different keywords).
- Top-N queries request at most 20 keywords.
- Keywords with identical frequencies may be returned in any order.

---

## Skills Demonstrated

- C++
- Advanced Data Structures
- Fibonacci Heap
- Hash Tables
- Priority Queues
- Amortized Analysis
- Algorithm Design
- File Processing
- Memory Management

---

## Coursework

Developed as part of:

**COP 5536 – Advanced Data Structures**  
**University of Florida**

The objective of the project was to design and implement an efficient keyword counting system capable of processing large streams of updates while supporting fast retrieval of the most popular keywords using advanced data structures.
