# Sudoku

This is a sudoku puzzle assignment for Artificial Intelligence module. 
One has to build a Sudoku solver in python. The sudoku puzzles are categorized into 4 cases : very easy, easy, medium, hard
Each of the test cases are given maximum 20secs to solve, a benchmark to count as successful. Any test cases that exceeded the given time frame will be timed-out.

## Algorithm & Constraints Approaches

There are a lot of algorithms approaches to solve the puzzle. I have chosen to go for backtracking ([Chaturvedi](#reference), 2021) approach - a combination of depth-first-search and simple constraints satisfaction. In short, backtracking is a technique to build a solution step by step. If at any point in sudoku puzzle, we realize that there's no valid solution in current cell, we will return to previous cell and alter the solution for that cell.

Detailed steps in building up the backtracking algorithm is as follow:

1. Scan through the board and look for empty cell (0) row by row.
2. Fill the cell with a random number (1-9). If a valid number is found, we would presume that the cell is correct and completed.
3. Then we will move on to next cell and repeat the action in Step 2.
4. Keep repeating until we encounter a cell with no valid numbers from 1-9.
5. The agent will move back to previous cell and try next valid numbers.
6. Repeat step 2-5 until there is no more empty cell (0) in the puzzle. The puzzle is solved!

However, several constraints have to be implemented along the backtracking algorithm in order to ensure the sudoku solver works successfully.

1. Only numbers of 1-9 is allowed to fill into the empty cell.
2. Each row, column and box (3x3) can only contain a unique number of 1-9. No duplication is allowed.
3. There are possibilities of sudoku puzzles with invalid_initial_states (same number appears more than 2 times either in row, column or box 3x3). 
4. Hence, validity of the board/puzzle is checked at early stage.

## Code and Functions

board_is_valid() - Checking the board at initial state to ensure that no duplication occurs. If any of the cell in row, column and box (3x3) appears to have any of the number 1-9 of more than 2 times, (0 is excepted), the puzzle is invalid. Return false.

invalid_initial() - If the board is invalid or no solution found in the board. The puzzle will return -1.

box_subgrid() - To create a sudoku box sub-grid of 3x3

is_valid() - To confirm if a given number from 1-9 is a valid option for a particular board cell. 3 requirements have to be satisfied:

1. None of the cell in row should contain the examined number.
2. None of the cell in column should contain the examined number.
3. None of the cell in box (3x3) should contain the examined number.

find_empty() - To find the entry in the still not in used/ empty. Return the reference location in parameter of row, col of the empty cell. In case it finds no empty cell, this is an indication that our puzzle/board is fully occupied and solved. Return a None value.

backtracking() - Steps as follow:

1. look for empty cell. If none is found, then puzzled solved.
2. If there's an empty cell, apply a number from 1-9 to that empty cell and examine if it's within our define constraints, a valid solution.
3. If the number is valid, call the backtracking() recursively and go back to step 1 to look for next empty cell.
4. If none of the number is valid, previous call of the function will reset the value of the cell to 0 and look for next valid number.

sudoku_solver() - Check if the initial state of the board is valid (satisfy 'no duplication' condition). If true, perform the backtracking and solve the puzzle. If puzzle is invalid or no solution, call invalid_initial(), puzzle/board returns 9x9 array of "-1".

## Results and Improvements

This is a simple backtracking approach with minimum constraints condition. The results turn out to be very effective on test cases from very easy to medium with less than 0.1 second. However, almost half of the test cases in hard took more than 20 secs to solve the puzzle. This can be further improved with more Constraint Propagation such as Single-value approach, elimination and naked twins. In conclusion, this is a fun and interesting assignments and a very good start learning the algorithm.

## Reference

Chaturvedi, A., 2021. Backtracking | Introduction - GeeksforGeeks. [online] GeeksforGeeks. Available from: {[https://www.geeksforgeeks.org/backtracking-introduction/](https://www.geeksforgeeks.org/backtracking-introduction/)} [Accessed 20 Mar. 2022].