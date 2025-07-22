
# 🔧 Mini-Project Solutions: Mathematical Thinking in Code

This document provides clean, well-commented solutions to the three mini-projects introduced in the final lesson: Maze Pathfinder, Simple Data Analyzer, and Image Filter.

---

## 1️⃣ Maze Pathfinder (Using Breadth-First Search - BFS)

### Problem:
Given a 2D maze, find the shortest path from the start point `S` to the end point `E`.

### Solution:

```python
from collections import deque

# Sample maze (S=start, E=end, '#'=wall, ' '=open path)
maze = [
    ['#', '#', '#', '#', '#', '#', '#', '#'],
    ['#', 'S', '#', ' ', ' ', ' ', 'E', '#'],
    ['#', ' ', '#', ' ', '#', ' ', '#', '#'],
    ['#', ' ', ' ', ' ', ' ', ' ', '#', '#'],
    ['#', '#', '#', '#', '#', '#', '#', '#']
]

def bfs_maze(maze):
    rows, cols = len(maze), len(maze[0])
    start = None
    for r in range(rows):
        for c in range(cols):
            if maze[r][c] == 'S':
                start = (r, c)

    queue = deque([(start, [])])  # (current_position, path_taken)
    visited = set()

    while queue:
        (r, c), path = queue.popleft()
        if maze[r][c] == 'E':
            return path + [(r, c)]

        for dr, dc in [(-1,0), (1,0), (0,-1), (0,1)]:
            nr, nc = r + dr, c + dc
            if (0 <= nr < rows and 0 <= nc < cols and 
                maze[nr][nc] != '#' and (nr, nc) not in visited):
                queue.append(((nr, nc), path + [(r, c)]))
                visited.add((nr, nc))

    return []

path = bfs_maze(maze)
print("Shortest path:", path)
```

---

## 2️⃣ Simple Data Analyzer (Using Statistics)

### Problem:
Read numbers from a file or list and compute:
- Mean
- Median
- Mode
- Variance

### Solution:

```python
import statistics

# Sample dataset (can be loaded from file)
data = [4, 5, 2, 7, 5, 6, 8, 5, 4, 6]

mean = statistics.mean(data)
median = statistics.median(data)
mode = statistics.mode(data)
variance = statistics.variance(data)

print("Mean:", mean)
print("Median:", median)
print("Mode:", mode)
print("Variance:", variance)
```

---

## 3️⃣ Image Filter (Basic Blur using Pillow)

### Problem:
Apply a basic image filter (e.g., blur) to an image using matrix operations.

### Solution:

```python
from PIL import Image, ImageFilter

# Load image
img = Image.open("sample.jpg")

# Apply blur filter
blurred_img = img.filter(ImageFilter.BLUR)

# Save or show result
blurred_img.show()  # Or blurred_img.save("blurred_output.jpg")
```

### Notes:
- For sharpening: use `ImageFilter.SHARPEN`
- For edge detection: use `ImageFilter.FIND_EDGES`

---

## ✅ Summary

| Project         | Key Math Used              | Python Tools        |
|----------------|----------------------------|---------------------|
| Maze Pathfinder| Graphs, BFS                | `collections.deque` |
| Data Analyzer  | Mean, Median, Mode, Var    | `statistics`        |
| Image Filter   | Matrix transforms          | `Pillow (PIL)`      |

These projects connect foundational math to real-world programming problems, and are excellent for reinforcing algorithmic thinking and data manipulation skills.