<h1 align="center">Word Count using MapReduce in Python</h1>

<p align="center">
An implementation of the Word Count problem using the MapReduce programming model in Python.
</p>

---

## Overview

This project demonstrates the Word Count problem using the MapReduce paradigm. It processes a given text input and counts the frequency of each word by dividing the task into three main phases: Mapper, Shuffle, and Reducer.

The implementation is written in Python to simulate how MapReduce works in distributed systems.

---

## Features

* Clear implementation of Mapper, Shuffle, and Reducer phases
* Displays intermediate outputs at each stage
* Simple and readable Python code
* Suitable for academic learning and demonstrations

---

## MapReduce Workflow

### Mapper

* Processes input text
* Converts words into key-value pairs
* Output format: (word, 1)

### Shuffle

* Groups all values by their keys
* Example:

  * hello → [1, 1]
  * world → [1, 1]

### Reducer

* Aggregates values for each key
* Produces final word counts

---

## Implementation

```python
def mapper(text):
    words = text.split()
    mapped = [(word.lower(), 1) for word in words]

    print("\n--- Mapper Output ---")
    for pair in mapped:
        print(pair)

    return mapped


def shuffle(mapped_data):
    shuffled = {}
    for word, count in mapped_data:
        if word not in shuffled:
            shuffled[word] = []
        shuffled[word].append(count)

    print("\n--- Shuffle Output ---")
    for key, value in shuffled.items():
        print(f"{key} : {value}")

    return shuffled


def reducer(shuffled_data):
    reduced = {}
    for word, counts in shuffled_data.items():
        reduced[word] = sum(counts)

    print("\n--- Reducer Output ---")
    for key, value in reduced.items():
        print(f"{key} : {value}")

    return reduced


text = "Hello world hello MapReduce world"

print("Input Text:", text)

mapped = mapper(text)
shuffled = shuffle(mapped)
result = reducer(shuffled)
```

---

## Example Output

### Mapper Output

```
('hello', 1)
('world', 1)
('hello', 1)
('mapreduce', 1)
('world', 1)
```

### Shuffle Output

```
hello : [1, 1]
world : [1, 1]
mapreduce : [1]
```

### Reducer Output

```
hello : 2
world : 2
mapreduce : 1
```

---

## How to Run

1. Save the file as `word_count.py`
2. Run the script:

```
python word_count.py
```

---

## Use Cases

* Understanding MapReduce concepts
* Academic assignments and lab work
* Demonstrating distributed data processing logic

---

## Author

Krishnendu M V

---

## License

This project is open-source and available under the MIT License.
