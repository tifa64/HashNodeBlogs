---
title: "Template for solving Backtracking Problems"
datePublished: Mon Dec 16 2024 16:42:54 GMT+0000 (Coordinated Universal Time)
cuid: cm4r9jz6400000ajs1knlghdg
slug: template-for-solving-backtracking-problems
tags: problem-solving, interview-questions

---

Inspired by [this Leetcode Post](https://leetcode.com/problems/permutations/solutions/18239/a-general-approach-to-backtracking-questions-in-java-subsets-permutations-combination-sum-palindrome-partioning/)

I've decided to provide a unified template and discussion for backtracking problems:

Here is a **Backtracking** template in **pseudo code**:

### Pseudo Code Template for Backtracking:

```plaintext
Function Backtrack(State, solution):
    // Base case: check if the solution is complete or valid
    if IsComplete(solution):
        // Process the solution if it's valid
        ProcessSolution(solution)
        return
    
    // Loop through possible options at this state
    for each option in GetOptions(State):
        // Make a choice and update the state
        MakeChoice(State, option)
        
        // Recursively explore further with the updated state
        Backtrack(UpdatedState, UpdatedSolution)
        
        // Undo the choice (Backtrack) to explore other options
        UndoChoice(State, option)

Function Main():
    // Define the initial state and solution
    InitialState = DefineInitialState()
    InitialSolution = InitializeSolution()
    
    // Start the backtracking process
    Backtrack(InitialState, InitialSolution)
```

### Explanation:

1. **Base Case**:  
    The function checks whether the current partial solution is complete or valid. If it is, the solution is processed (e.g., printed, stored, or counted), and the recursion stops for this branch.
    
2. **Explore Options**:  
    The function loops through each possible option or decision at the current state. For each option, it updates the state, makes a choice, and proceeds to the next step recursively.
    
3. **Make a Choice**:  
    This step modifies the current state based on the option chosen, like adding an element to a solution or choosing a path.
    
4. **Undo the Choice (Backtrack)**:  
    After exploring one possibility (or even after exploring further down the recursion tree), the algorithm backtracks by undoing the previous choice, reverting the state back to what it was before. This ensures that other options can be explored.
    
5. **Recursive Call**:  
    The function makes a recursive call to explore the next level of decisions using the updated state and solution.
    
6. **Main Function**:  
    The `Main()` function initializes the starting state and solution, then triggers the backtracking process by calling `Backtrack()`.
    

---

### Example Problem: N-Queens Problem

This is an example of using the backtracking template to solve the **N-Queens problem**, where the goal is to place N queens on an N×N chessboard such that no two queens threaten each other.

```plaintext
Function IsSafe(board, row, col):
    // Check if placing a queen at (row, col) is safe
    for each i from 0 to row-1:
        if board[i][col] == 1:  // Check the column
            return False
        if board[i][col - (row - i)] == 1:  // Check the left diagonal
            return False
        if board[i][col + (row - i)] == 1:  // Check the right diagonal
            return False
    return True

Function Backtrack(board, row):
    // Base case: if all queens are placed
    if row == N:
        ProcessSolution(board)
        return
    
    // Try placing a queen in each column for this row
    for col from 0 to N-1:
        if IsSafe(board, row, col):
            board[row][col] = 1  // Place a queen
            Backtrack(board, row + 1)  // Recursively place queens in the next row
            board[row][col] = 0  // Undo the choice (backtrack)

Function ProcessSolution(board):
    // Output the current solution (board configuration)
    Print(board)

Function Main():
    N = 4  // Size of the board (4x4 in this example)
    board = InitializeBoard(N)
    Backtrack(board, 0)
```

### Key Functions in the Example:

* **IsSafe(board, row, col)**: This checks if placing a queen at position `(row, col)` is safe by ensuring no other queens are in the same column or diagonal.
    
* **Backtrack(board, row)**: The main backtracking function that places queens row by row. It attempts to place a queen in each column of the current row, then recursively tries to place queens in the following rows. If placing a queen leads to a valid solution, it processes the board; otherwise, it backtracks by removing the queen and trying the next column.
    
* **ProcessSolution(board)**: This function is called when a valid arrangement of queens is found, and it outputs the solution.
    

---

### Example Problem: Subset Sum Problem

Here's another example that solves the **Subset Sum** problem, where we want to find a subset of numbers that adds up to a given target.

```plaintext
Function Backtrack(nums, target, index, currentSubset):
    // Base case: if target becomes 0, we found a solution
    if target == 0:
        ProcessSolution(currentSubset)
        return
    
    // Base case: if index exceeds the array size or target becomes negative
    if index >= length(nums) or target < 0:
        return
    
    // Include the current number and recurse
    currentSubset.append(nums[index])
    Backtrack(nums, target - nums[index], index + 1, currentSubset)
    
    // Exclude the current number and recurse
    currentSubset.removeLast()
    Backtrack(nums, target, index + 1, currentSubset)

Function ProcessSolution(currentSubset):
    // Output the current solution (subset)
    Print(currentSubset)

Function Main():
    nums = [2, 3, 7, 8, 10]
    target = 11
    Backtrack(nums, target, 0, [])
```

### Key Functions in this Example:

* **Backtrack(nums, target, index, currentSubset)**: This function tries to find a subset of numbers from `nums` that adds up to `target`. It does this by including the current number, recursing, and then backtracking by excluding it.
    
* **ProcessSolution(currentSubset)**: When a valid subset is found, this function processes it (e.g., printing the subset).
    

---

### Key Points:

* **Recursive exploration**: In backtracking, each choice leads to a recursive call exploring the next step.
    
* **Undo choices**: After exploring one path, backtracking undoes the current decision (by removing the item or reversing the choice) to explore a different path.
    
* **Base case**: When the solution is complete or no more choices can be made, the algorithm terminates or processes the solution.
    

Backtracking is commonly used for problems where you need to explore all possible combinations or configurations and choose the best one (or all valid solutions), such as in puzzles, combinatorial problems, or constraint satisfaction problems.

### Generalized Backtracking Template:

```java
public List<List<Integer>> solveProblem(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);  // Sort if needed (for problems like subsets, permutations with duplicates)
    backtrack(result, new ArrayList<>(), nums, 0);  // Start backtracking
    return result;
}

private void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] nums, int start) {
    // Base Case: Add the current tempList to result if needed (for subsets, combinations, etc.)
    result.add(new ArrayList<>(tempList));
    
    // Iterate through the numbers starting from 'start'
    for (int i = start; i < nums.length; i++) {
        // Handle duplicate cases if necessary
        if (i > start && nums[i] == nums[i-1]) continue; // Skip duplicate elements
        
        // Choose the current number
        tempList.add(nums[i]);
        
        // Explore further (backtracking)
        backtrack(result, tempList, nums, i + 1);  // Adjust 'i+1' or 'i' based on problem constraints
        
        // Undo the choice (backtrack)
        tempList.remove(tempList.size() - 1);
    }
}
```

### Observations on the Provided Problems:

1. **Subsets (No duplicates)**:
    
    * Standard backtracking with an iterative approach to generate all subsets of the given array.
        
    * The `start` index ensures that we never repeat subsets, and after each addition, we backtrack to explore other possibilities.
        
2. **Subsets II (Contains duplicates)**:
    
    * Similar to the previous problem but includes a check to skip duplicates.
        
    * This is necessary because sorting the array helps us detect duplicates, so if we encounter the same element consecutively, we skip it.
        
3. **Permutations (No duplicates)**:
    
    * We generate all permutations by picking elements from the array and ensuring that no element is repeated within a permutation.
        
    * `tempList.contains(nums[i])` is used to check if an element has already been used.
        
4. **Permutations II (Contains duplicates)**:
    
    * This problem is similar to the previous one but handles duplicates.
        
    * We also use a `used[]` array to track which elements are already used in the current permutation.
        
    * An additional condition `if(i > 0 && nums[i] == nums[i-1] && !used[i - 1])` ensures that we don’t use a duplicate element in the same permutation.
        
5. **Combination Sum (Reuse elements allowed)**:
    
    * This problem allows elements to be reused, so we pass `i` (not `i + 1`) to ensure that the current element can be reused in the next step of the recursion.
        
    * The key is checking if the remaining sum (`remain`) is less than 0 or equal to 0.
        
6. **Combination Sum II (No reuse of elements)**:
    
    * Similar to the previous one but disallows reuse of elements.
        
    * We skip duplicates by checking `if(i > start && nums[i] == nums[i-1]) continue;` to avoid reusing the same element in the same position.
        
7. **Palindrome Partitioning**:
    
    * The problem requires partitioning a string into substrings where each substring is a palindrome.
        
    * We use the helper function `isPalindrome` to check if a substring is a palindrome.
        
    * The recursion ensures that we generate all possible partitions, and backtracking is used to remove the last added substring after exploring all possibilities.
        

### General Observations:

* **Sorting**: Sorting the array at the start is common in problems like subsets and permutations to handle duplicates and simplify decision-making.
    
* **Backtracking Pattern**: The common pattern for backtracking includes:
    
    1. **Choose**: Add an element to the current solution (`tempList`).
        
    2. **Explore**: Recursively explore further choices.
        
    3. **Undo**: Remove the last element to try different paths.
        
* **Handling Duplicates**: Duplicates are managed by either skipping identical consecutive elements in a sorted array (for subsets and permutations) or tracking used elements (for permutations).
    
* **Base Cases**: For problems like combination sum, subsets, and palindrome partitioning, the base cases typically involve checking if a valid solution has been found (e.g., remaining sum is zero or we’ve partitioned the string completely).
    

### Key Customizations:

* **Start index**: Controls whether you allow reusing elements or not. In most problems like combination sum and permutations, the `start` index helps guide the recursion correctly.
    
* **Base conditions**: These are problem-specific and include conditions like the length of `tempList`, checking the remaining sum, or the end of the string.
    

### In backtracking, when should I loop and when shouldn't I loop ?

In backtracking, the decision to loop or not depends on the nature of the problem you're solving. Let's break it down by discussing when you typically **should loop** and when you **shouldn't loop** during backtracking.

### When **You Should Loop**:

1. **Exploring Choices**:
    
    * You loop when you have a set of choices or decisions to make at each step, and you need to try each option one by one. This is common in problems like **subsets**, **permutations**, and **combinations**, where you have multiple elements to choose from at each recursive step.
        
    * For example, in **combinations** or **subsets**, you might loop through the array of numbers to decide whether to include each element in the current subset or combination.
        
    
    ```java
    for (int i = start; i < nums.length; i++) {
        // Make a choice (e.g., adding nums[i] to the current list)
        tempList.add(nums[i]);
        // Recurse (explore further choices)
        backtrack(result, tempList, nums, i + 1);
        // Undo the choice (backtrack)
        tempList.remove(tempList.size() - 1);
    }
    ```
    
2. **Exploring Multiple Paths**:
    
    * When you have multiple ways to explore (i.e., multiple branches in the decision tree), you loop to explore each of these options. For example, in **permutations**, you might loop through all elements, picking one at each recursive step, ensuring you don’t repeat elements unless specified (like in **Permutations II** with duplicates).
        
3. **Generating All Solutions**:
    
    * When generating all possible solutions (e.g., in **subsets**, **combinations**, **permutations**), you loop to explore all possible subsets/choices by considering every possibility, including skipping some elements or choosing certain elements multiple times (if allowed).
        

### When **You Shouldn’t Loop**:

1. **Single Decision Point**:
    
    * When you're dealing with a problem where there’s only one decision to make at each step, looping isn’t needed. For instance, in **Palindrome Partitioning**, you don't need to loop over the characters at every step because the next step is deterministic (you just need to check whether the current substring is a palindrome).
        
    
    ```java
    if (isPalindrome(s, start, i)) {
        tempList.add(s.substring(start, i + 1));
        backtrack(result, tempList, s, i + 1);
        tempList.remove(tempList.size() - 1);
    }
    ```
    
2. **Pruning / Early Termination**:
    
    * In some cases, you might not need to loop if you have a condition that prunes the search space or eliminates paths early. For example, if you're solving a **knapsack problem** or **subset sum problem** where the sum exceeds a target value, you may not need to explore further once you've passed a certain threshold.
        
    * **Base cases** are often used to stop further recursion (like when a subset’s sum exceeds the target in **Combination Sum** or when the string is completely partitioned in **Palindrome Partitioning**).
        
3. **When You Have a Deterministic Path**:
    
    * If there's only one possible solution to explore from a particular state, looping through multiple elements is unnecessary. This can happen in **constraint satisfaction problems** where the path is largely dictated by earlier choices (e.g., a Sudoku solver, where the next step is always determined based on prior steps).
        
4. **Backtracking with a Fixed Set of Choices**:
    
    * In some backtracking problems like **n-queens**, you may only loop through rows or columns at a fixed position, but once the current position is fixed, there's no need to loop through other options. The backtracking decision tree itself will guide you to the next step.
        

### Example to Illustrate the Decision to Loop or Not:

Consider the **Combination Sum II** problem:

```java
public List<List<Integer>> combinationSum2(int[] nums, int target) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);  // Sorting helps in skipping duplicates
    backtrack(result, new ArrayList<>(), nums, target, 0);
    return result;
}

private void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] nums, int remain, int start) {
    if (remain < 0) return;  // Pruning, no need to continue if remain is negative
    else if (remain == 0) {
        result.add(new ArrayList<>(tempList));  // Solution found
        return;
    }
    for (int i = start; i < nums.length; i++) {
        // Skip duplicates to avoid repeating the same combination
        if (i > start && nums[i] == nums[i - 1]) continue;

        tempList.add(nums[i]);
        backtrack(result, tempList, nums, remain - nums[i], i + 1);  // Loop to explore the next choices
        tempList.remove(tempList.size() - 1);  // Undo the choice
    }
}
```

* **Loop**: You loop over `nums` from `start` to explore all possible numbers that can be added to the current combination. This ensures that you generate all possible combinations.
    
* **Pruning/Stopping the Loop**: If the remaining target becomes negative, you stop the loop and return because no valid combination can be found from this point.
    
* **Skipping Duplicates**: If the current element is the same as the previous one (and isn't the first occurrence), you skip it to avoid generating duplicate combinations.
    

### Key Takeaways:

* **When to Loop**: Use a loop when you have multiple decisions to make, need to explore different choices, or need to generate all possible solutions (e.g., subsets, permutations).
    
* **When Not to Loop**: Avoid unnecessary looping when there is only one possible path (like in palindromes) or when the search space can be pruned early through base cases or constraints.
    

## When there is a need to loop through an array, sometimes the starting point of the array is 0 and sometimes it is index where index is a parameter to be passed in the backtracking function. When should the i start at 0 and when should it start at index?

Here’s the explanation and examples rewritten in Java with code snippets:

---

### **Explanation**

When solving backtracking problems where you loop through an array, the starting point of the loop depends on the requirements of the problem:

1. **Start at** `0`:  
    Use this when elements can be reused in every recursive call, and the order matters. This is typically used in:
    
    * **Permutations**: You generate all possible arrangements of elements, considering order.
        
    * **Combinations with replacement**: You are allowed to use the same element multiple times in different combinations (e.g., selecting coins for a total amount).
        
2. **Start at** `index`:  
    Use this when elements before `index` should not be revisited in the current path. This is typically used in:
    
    * **Combinations without replacement**: Selecting unique subsets where the order doesn’t matter.
        
    * **Avoiding duplicates**: Ensuring combinations are generated in a forward direction to avoid redundant subsets.
        

---

### **Combination with Replacement**

In combinations with replacement, you are allowed to reuse the same element multiple times. For example, if the input array is `{1, 2, 3}` and you want combinations of size `2`, the result would be:  
`{1, 1}, {1, 2}, {1, 3}, {2, 2}, {2, 3}, {3, 3}`.

---

### **Java Code Examples**

#### **1\. Permutations (Start at** `0`)

```java
import java.util.*;

public class Permutations {
    public static void permute(int[] nums, List<Integer> path, boolean[] used) {
        if (path.size() == nums.length) {
            System.out.println(path);
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) continue; // Skip already used elements
            used[i] = true;        // Mark element as used
            path.add(nums[i]);     // Add to current path
            permute(nums, path, used);
            path.remove(path.size() - 1); // Backtrack
            used[i] = false;       // Unmark the element
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        permute(nums, new ArrayList<>(), new boolean[nums.length]);
    }
}
```

---

#### **2\. Combinations without Replacement (Start at** `index`)

```java
import java.util.*;

public class Combinations {
    public static void combine(int[] nums, int index, List<Integer> path) {
        System.out.println(path); // Print valid combination
        for (int i = index; i < nums.length; i++) {
            path.add(nums[i]);     // Add current element
            combine(nums, i + 1, path); // Move to the next index
            path.remove(path.size() - 1); // Backtrack
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        combine(nums, 0, new ArrayList<>());
    }
}
```

---

#### **3\. Combinations with Replacement (Start at** `index`)

```java
import java.util.*;

public class CombinationWithReplacement {
    public static void combineWithReplacement(int[] nums, int index, List<Integer> path) {
        System.out.println(path); // Print valid combination
        for (int i = index; i < nums.length; i++) {
            path.add(nums[i]);           // Add current element
            combineWithReplacement(nums, i, path); // Allow reuse of the same element
            path.remove(path.size() - 1); // Backtrack
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        combineWithReplacement(nums, 0, new ArrayList<>());
    }
}
```

---

### **Key Points**

1. **Permutations**: Loop starts at `0` because every element can be used in any position, but an additional check is needed to avoid reusing elements already in the current path.
    
2. **Combinations without Replacement**: Loop starts at `index` because we only consider elements forward of the current index to avoid duplicates.
    
3. **Combinations with Replacement**: Loop starts at `index`, but we allow the same element to be reused in the recursive call by not incrementing the starting index.
    

---

### **Combination with Replacement Example**

For the array `{1, 2, 3}`, if you want all combinations of size `2`:

* Start at `index` to avoid duplicates.
    
* Allow reuse of the same element by recursively calling with the same starting `index`.
    

The result would be:  
`{1, 1}, {1, 2}, {1, 3}, {2, 2}, {2, 3}, {3, 3}`.

The **combinations with replacement** logic allows picking the same element multiple times while maintaining sorted order to prevent duplicate subsets.

## When should we pass index+1 in the recursive call, when should we pass i+1 and when should we pass i?

The choice of whether to pass `index + 1`, `i + 1`, or `i` in the recursive call depends on the problem and the rules governing the backtracking algorithm. Here's an explanation for each case:

---

### **1\. Pass** `index + 1`

You pass `index + 1` when you want to start the next recursive call from the element **immediately after the current starting index**, regardless of the current loop variable (`i`). This is used when:

* The starting point for exploration is fixed based on a specific `index` variable (like a parameter passed to the function).
    
* The current loop variable (`i`) is not tied directly to how the recursion progresses.
    

#### **Example Use Case: Generating Subsequences**

```java
public static void generateSubsequences(int[] nums, int index, List<Integer> path) {
    System.out.println(path); // Print current subsequence
    for (int i = index; i < nums.length; i++) {
        path.add(nums[i]); // Include current element
        generateSubsequences(nums, i + 1, path); // Move to the next index
        path.remove(path.size() - 1); // Backtrack
    }
}
```

Here, `index + 1` ensures that each recursive call only considers elements after the current one, generating all subsequences without revisiting earlier elements.

---

### **2\. Pass** `i + 1`

You pass `i + 1` when you want to start the next recursive call **immediately after the current element** in the current iteration. This is used when:

* The recursion depends directly on the current loop variable (`i`).
    
* You want to avoid revisiting the current element in subsequent recursive calls.
    

#### **Example Use Case: Combinations Without Replacement**

```java
public static void combine(int[] nums, int index, List<Integer> path) {
    System.out.println(path); // Print current combination
    for (int i = index; i < nums.length; i++) {
        path.add(nums[i]); // Add current element
        combine(nums, i + 1, path); // Move to the next element in the loop
        path.remove(path.size() - 1); // Backtrack
    }
}
```

Here, `i + 1` ensures that the next recursive call skips over the current element and only processes elements that come after it in the array.

---

### **3\. Pass** `i`

You pass `i` when you want to allow the recursion to **reuse the current element**. This is used in cases where:

* Repetition of the same element is allowed (e.g., combinations with replacement).
    
* You need to stay on the current element and explore further possibilities before moving forward.
    

#### **Example Use Case: Combinations With Replacement**

```java
public static void combineWithReplacement(int[] nums, int index, List<Integer> path) {
    System.out.println(path); // Print current combination
    for (int i = index; i < nums.length; i++) {
        path.add(nums[i]); // Add current element
        combineWithReplacement(nums, i, path); // Allow reuse of the same element
        path.remove(path.size() - 1); // Backtrack
    }
}
```

Here, passing `i` ensures that the same element can be reused in the recursive call, which is essential for combinations with replacement.

---

### **Summary**

| Case | Pass `index + 1` | Pass `i + 1` | Pass `i` |
| --- | --- | --- | --- |
| **When to use** | Start after the initial index regardless of the loop. | Skip the current element in the loop and move forward. | Allow reuse of the current element. |
| **Example Problems** | Generating subsequences, subsets. | Combinations without replacement, avoiding duplicates. | Combinations with replacement, repetitions allowed. |
| **Purpose** | Progress the recursion based on a fixed index. | Skip the current element and proceed. | Stay on the current element to allow repetition. |

---

### **Examples for Clarity**

#### **1\. Passing** `index + 1`

* Input: `{1, 2, 3}`
    
* Output: Generate all **subsequences**:  
    `{}, {1}, {1, 2}, {1, 3}, {1, 2, 3}, {2}, {2, 3}, {3}`
    

#### **2\. Passing** `i + 1`

* Input: `{1, 2, 3}`
    
* Output: Generate all **combinations without replacement**:  
    `{1, 2}, {1, 3}, {2, 3}`
    

#### **3\. Passing** `i`

* Input: `{1, 2, 3}`
    
* Output: Generate all **combinations with replacement**:  
    `{1, 1}, {1, 2}, {1, 3}, {2, 2}, {2, 3}, {3, 3}`
    

---

Hope you find this useful 😊