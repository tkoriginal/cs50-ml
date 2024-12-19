# Movie Database Search and Maze Solver

This project contains two main components: a movie database search algorithm and a maze solver. It demonstrates various search techniques in artificial intelligence.

The movie database search allows users to find the shortest connection between two actors through the movies they've starred in, similar to the "Six Degrees of Kevin Bacon" game. The maze solver implements a breadth-first search algorithm to find the optimal path through a maze.

These components showcase different applications of search algorithms in solving real-world problems and navigating complex data structures.

## Repository Structure

```
.
└── 01-Search
    ├── code
    │   └── maze.py
    └── degrees
        ├── degrees.py
        └── util.py
```

### Key Files

- `01-Search/code/maze.py`: Contains the implementation of the maze solver.
- `01-Search/degrees/degrees.py`: Implements the movie database search functionality.
- `01-Search/degrees/util.py`: Provides utility classes for the search algorithms.

## Usage Instructions

### Prerequisites

- Python 3.6 or higher

### Installation

1. Clone the repository:
   ```
   git clone <repository-url>
   cd 01-Search
   ```

2. No additional dependencies are required for this project.

### Maze Solver

To run the maze solver:

```
python code/maze.py <maze_file>
```

Replace `<maze_file>` with the path to a text file containing the maze layout. The maze file should use the following format:
- 'A' represents the starting point
- 'B' represents the goal
- '#' or any non-space character represents walls
- ' ' (space) represents open paths

Example:
```
python code/maze.py maze.txt
```

The program will output:
1. The initial maze layout
2. The solution path
3. The number of states explored
4. An image file (`maze.png`) showing the maze and the solution path

### Movie Database Search

To run the movie database search:

```
python degrees/degrees.py [directory]
```

The `[directory]` argument is optional and defaults to "large". It should contain the following CSV files:
- `people.csv`: Contains information about people in the database
- `movies.csv`: Contains information about movies
- `stars.csv`: Contains information about which actors starred in which movies

The program will prompt you to enter two names, and it will find the shortest path between them through shared movie appearances.

Example:
```
python degrees/degrees.py
Name: Emma Watson
Name: Jennifer Lawrence
3 degrees of separation.
1: Emma Watson and Brendan Gleeson starred in Harry Potter and the Order of the Phoenix
2: Brendan Gleeson and Michael Fassbender starred in Trespass Against Us
3: Michael Fassbender and Jennifer Lawrence starred in X-Men: First Class
```

## Data Flow

The data flow in both components follows a similar pattern:

1. Input Processing:
   - Maze Solver: Reads the maze layout from a file.
   - Movie Search: Loads data from CSV files into memory.

2. Search Initialization:
   - Maze Solver: Creates a start node at the 'A' position.
   - Movie Search: Converts input names to person IDs.

3. Search Algorithm:
   - Both use a breadth-first search implemented with a queue frontier.
   - Explores nodes, tracking visited states to avoid cycles.

4. Goal Check:
   - Maze Solver: Checks if current position is 'B'.
   - Movie Search: Checks if current person is the target.

5. Path Construction:
   - When goal is reached, constructs the path by backtracking through parent nodes.

6. Output:
   - Maze Solver: Prints maze, solution path, and generates an image.
   - Movie Search: Prints the degrees of separation and the connecting movies.

```
[Input] -> [Load Data] -> [Initialize Search] -> [Search Algorithm] -> [Goal Check] -> [Path Construction] -> [Output]
```

## Troubleshooting

### Common Issues

1. FileNotFoundError when running the maze solver:
   - Ensure the maze file exists and the path is correct.
   - Check your current working directory.

2. KeyError in the movie database search:
   - Verify that the CSV files in the specified directory are complete and correctly formatted.
   - Ensure the names you're searching for exist in the database.

### Debugging

To enable debug mode for the movie database search:
1. Open `degrees/degrees.py`
2. Add `import logging` at the top of the file
3. Add the following lines before the `load_data` function call in `main()`:
   ```python
   logging.basicConfig(level=logging.DEBUG)
   logging.debug("Debug mode enabled")
   ```
4. Run the script as usual. You will now see detailed debug information in the console.

For the maze solver, you can add print statements in the `solve` method of the `Maze` class to track the search progress.

### Performance Optimization

If the movie database search is slow:
1. Profile the code using cProfile:
   ```
   python -m cProfile -o output.prof degrees/degrees.py
   ```
2. Analyze the output with a tool like snakeviz:
   ```
   snakeviz output.prof
   ```
3. Look for bottlenecks in data loading or the search algorithm.

For large mazes, consider implementing an A* search algorithm in `maze.py` to improve performance.