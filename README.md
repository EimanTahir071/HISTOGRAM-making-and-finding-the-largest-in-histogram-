# Histogram - Making and Finding the Largest

A comprehensive guide and implementation for histogram creation and finding the largest rectangle in a histogram. This project covers fundamental data structure concepts and efficient algorithmic approaches to solve the classic histogram problem.

## Overview

This project addresses two core problems:

1. **Creating Histograms**: Building histogram data structures from raw data
2. **Largest Rectangle in Histogram**: Finding the maximum area rectangle within a histogram using optimal algorithms

## Problem Statement

### Largest Rectangle in Histogram

Given an array of heights representing a histogram, find the area of the largest rectangle that can be formed.

**Example:**
```
Heights: [2, 1, 5, 6, 2, 3]

Visual representation:
      |   |
  |   | | |
  | | | | | |
  ---------
  Area = 10 (height 5, width 2)
```

## Algorithms & Approaches

### 1. **Brute Force O(n²)**

For each position, expand left and right to find the maximum height, then calculate area.

```python
def largestRectangleBruteForce(heights):
    max_area = 0
    for i in range(len(heights)):
        min_height = heights[i]
        for j in range(i, len(heights)):
            min_height = min(min_height, heights[j])
            area = min_height * (j - i + 1)
            max_area = max(max_area, area)
    return max_area
```

### 2. **Stack-Based Approach O(n)** ⭐ Optimal

Uses a monotonic stack to track indices of increasing heights.

```python
def largestRectangle(heights):
    stack = []
    max_area = 0
    
    for i, h in enumerate(heights):
        start = i
        while stack and stack[-1][1] > h:
            idx, height = stack.pop()
            area = height * (i - idx)
            max_area = max(max_area, area)
            start = idx
        if h > 0:
            stack.append((start, h))
    
    for idx, height in stack:
        area = height * (len(heights) - idx)
        max_area = max(max_area, area)
    
    return max_area
```

### 3. **Divide & Conquer O(n log n)**

Find minimum height, divide array into segments, recursively solve.

## Files & Structure

```
.
├── src/
│   ├── histogram.py          # Core histogram implementations
│   ├── brute_force.py        # O(n²) solution
│   ├── stack_solution.py     # O(n) optimal solution
│   ├── divide_conquer.py     # O(n log n) solution
│   └── utils.py              # Helper functions
├── tests/
│   ├── test_histogram.py     # Unit tests
│   └── test_performance.py   # Benchmarks
├── notebooks/
│   └── visualization.ipynb   # Visual demonstrations
└── README.md
```

## Usage

### Basic Example

```python
from src.histogram import largestRectangle

heights = [2, 1, 5, 6, 2, 3]
result = largestRectangle(heights)
print(f"Largest rectangle area: {result}")  # Output: 10
```

### Running Tests

```bash
pytest tests/ -v
```

### Performance Comparison

```bash
python tests/test_performance.py
```

## Complexity Analysis

| Algorithm | Time | Space | Notes |
|-----------|------|-------|-------|
| Brute Force | O(n²) | O(1) | Simple but slow |
| Stack-Based | O(n) | O(n) | Optimal, recommended |
| Divide & Conquer | O(n log n) | O(log n) | Recursive overhead |

## Key Insights

1. **Monotonic Stack**: Maintaining increasing order helps avoid redundant comparisons
2. **Index Tracking**: Store indices, not just heights, to calculate widths
3. **Boundary Handling**: Process remaining stack elements at the end
4. **Space-Time Trade-off**: O(n) time requires O(n) space for the stack

## Real-World Applications

- **Chart/Graph Rendering**: Finding optimal display bounds
- **Image Processing**: Rectangle detection in histograms
- **Memory Allocation**: Finding largest contiguous block
- **Manufacturing**: Optimal cutting of materials

## Extended Problems

- **Maximal Rectangle in Matrix**: 2D variant (LeetCode 85)
- **Largest Rectangle under Skyline**: Variant with skyline constraint
- **Dynamic Histogram**: Updates and queries

## Testing

Test cases cover:

- Edge cases (empty, single element, all same)
- Increasing/decreasing sequences
- Large random datasets
- Performance benchmarks

```bash
pytest tests/test_histogram.py::test_edge_cases -v
```

## Resources

- [GeeksforGeeks - Largest Rectangle in Histogram](https://www.geeksforgeeks.org/largest-rectangle-in-histogram/)
- [LeetCode Problem 84](https://leetcode.com/problems/largest-rectangle-in-histogram/)
- Algorithm Textbooks: CLRS, Algorithm Design Manual

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add tests for new solutions
4. Submit a pull request

## License

MIT License - Feel free to use and modify for learning purposes.

---

**Last Updated**: February 2026
