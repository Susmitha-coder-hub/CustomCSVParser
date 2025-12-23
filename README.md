📌 Project Overview

This project implements a Custom CSV Reader and Writer in Python without using Python’s built-in csv module.
The goal is to manually handle:

Plain fields

Quoted fields

Escaped quotes ""

Newlines inside quoted fields

Streaming reading (no full-file loading)

In addition, a benchmarking script is provided to measure the performance of this custom implementation compared to the standard library.

📂 Project Structure
llm-retrieval-system/
│
├── custom_csv_reader.py
├── custom_csv_writer.py
├── reader_test.py
├── writer_test.py
├── reader_writer_test.py
├── benchmark.py
├── benchmark_results.json
└── README.md   ← (this file)

🛠 Installation / Requirements

Python: 3.8 or above

No external libraries required (pure Python)

Optional (for more testing): pytest

📖 Usage Examples
1. Writing to CSV using CustomCsvWriter
from custom_csv_writer import CustomCsvWriter

with open('example.csv', 'w', newline='', encoding='utf-8') as f:
    writer = CustomCsvWriter(f)
    writer.writerows([
        ['a', 'b,c', 'd"d'],
        ['x', 'y', 'z']
    ])

2. Reading CSV using CustomCsvReader
from custom_csv_reader import CustomCsvReader

with open('example.csv', 'r', encoding='utf-8') as f:
    reader = CustomCsvReader(f)
    for row in reader:
        print(row)

🧪 Testing

These tests verify correct CSV parsing:

✔ Basic fields
✔ Quoted fields
✔ Escaped quotes ("" → ")
✔ Newlines inside quoted fields
✔ Empty fields / trailing commas
✔ CRLF (\r\n) and LF (\n) newline support
✔ Malformed CSV error handling
✔ Cross-compatibility:

File created by CustomCsvWriter is readable by csv.reader

File created by csv.writer is readable by CustomCsvReader

Example test files:

reader_test.py

writer_test.py

reader_writer_test.py

⚡ Benchmarking

Run:

python benchmark.py


You will see results like:

---- CSV BENCHMARK RESULTS ----
Read Speed  : 0.001208 seconds
Write Speed : 0.000372 seconds

Benchmark results saved to benchmark_results.json


A JSON file benchmark_results.json is also created containing:

total read time

total write time

timestamps

📌 Benchmark Methodology

A synthetic CSV file is generated

10,000 rows × 5 columns

Mixed content: commas, quotes, newlines

Benchmarks:

CustomCsvReader vs csv.reader

CustomCsvWriter vs csv.writer

📊 Expected Results (Summary)

Because Python’s built-in csv module is implemented in C, it is expected to be:

Faster in most cases

More optimized for large files

However, this project demonstrates:

Full manual parsing

Character-by-character control

Correct CSV handling logic

🚧 Limitations & Future Improvements
Current limitations:

Using read(1) can be slower for huge files

Some advanced CSV edge cases not required by assignment are skipped

No dialect options (delimiter changes, quotechar, etc.)

Possible improvements:

Chunk-based buffered reading

Support for custom delimiters

Improved error messages

Faster string building using bytearray

👩‍💻 Author / Ownership

This project is developed as an educational implementation for learning:

Parsing logic

Streaming file processing

Custom CSV handling

Benchmarking techniques