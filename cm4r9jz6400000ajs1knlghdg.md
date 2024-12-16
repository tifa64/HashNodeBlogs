---
title: "Template for solving Backtracking Problems"
datePublished: Mon Dec 16 2024 16:42:54 GMT+0000 (Coordinated Universal Time)
cuid: cm4r9jz6400000ajs1knlghdg
slug: template-for-solving-backtracking-problems
tags: problem-solving, interview-questions

---

Inspired by [this Leetcode Post](https://leetcode.com/problems/permutations/solutions/18239/a-general-approach-to-backtracking-questions-in-java-subsets-permutations-combination-sum-palindrome-partioning/)

I've decided to provide a unified template and discussion for backtracking problems:


Here’s a generalized template for backtracking problems that you can use for solving similar problems like subsets, permutations, combination sum, and palindrome partitioning. I'll also provide some observations on each problem based on the given examples.

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
   - Standard backtracking with an iterative approach to generate all subsets of the given array.  
   - The `start` index ensures that we never repeat subsets, and after each addition, we backtrack to explore other possibilities.

2. **Subsets II (Contains duplicates)**:  
   - Similar to the previous problem but includes a check to skip duplicates.  
   - This is necessary because sorting the array helps us detect duplicates, so if we encounter the same element consecutively, we skip it.

3. **Permutations (No duplicates)**:  
   - We generate all permutations by picking elements from the array and ensuring that no element is repeated within a permutation.  
   - `tempList.contains(nums[i])` is used to check if an element has already been used.

4. **Permutations II (Contains duplicates)**:  
   - This problem is similar to the previous one but handles duplicates.  
   - We also use a `used[]` array to track which elements are already used in the current permutation.  
   - An additional condition `if(i > 0 && nums[i] == nums[i-1] && !used[i - 1])` ensures that we don’t use a duplicate element in the same permutation.

5. **Combination Sum (Reuse elements allowed)**:  
   - This problem allows elements to be reused, so we pass `i` (not `i + 1`) to ensure that the current element can be reused in the next step of the recursion.  
   - The key is checking if the remaining sum (`remain`) is less than 0 or equal to 0.

6. **Combination Sum II (No reuse of elements)**:  
   - Similar to the previous one but disallows reuse of elements.  
   - We skip duplicates by checking `if(i > start && nums[i] == nums[i-1]) continue;` to avoid reusing the same element in the same position.

7. **Palindrome Partitioning**:  
   - The problem requires partitioning a string into substrings where each substring is a palindrome.  
   - We use the helper function `isPalindrome` to check if a substring is a palindrome.  
   - The recursion ensures that we generate all possible partitions, and backtracking is used to remove the last added substring after exploring all possibilities.

### General Observations:
- **Sorting**: Sorting the array at the start is common in problems like subsets and permutations to handle duplicates and simplify decision-making.
- **Backtracking Pattern**: The common pattern for backtracking includes:
  1. **Choose**: Add an element to the current solution (`tempList`).
  2. **Explore**: Recursively explore further choices.
  3. **Undo**: Remove the last element to try different paths.
- **Handling Duplicates**: Duplicates are managed by either skipping identical consecutive elements in a sorted array (for subsets and permutations) or tracking used elements (for permutations).
- **Base Cases**: For problems like combination sum, subsets, and palindrome partitioning, the base cases typically involve checking if a valid solution has been found (e.g., remaining sum is zero or we’ve partitioned the string completely).

### Key Customizations:
- **Start index**: Controls whether you allow reusing elements or not. In most problems like combination sum and permutations, the `start` index helps guide the recursion correctly.
- **Base conditions**: These are problem-specific and include conditions like the length of `tempList`, checking the remaining sum, or the end of the string.
  
### In backtracking, when should I loop and when shouldn't I loop ?
In backtracking, the decision to loop or not depends on the nature of the problem you're solving. Let's break it down by discussing when you typically **should loop** and when you **shouldn't loop** during backtracking.

### When **You Should Loop**:
1. **Exploring Choices**:  
   - You loop when you have a set of choices or decisions to make at each step, and you need to try each option one by one. This is common in problems like **subsets**, **permutations**, and **combinations**, where you have multiple elements to choose from at each recursive step.
   - For example, in **combinations** or **subsets**, you might loop through the array of numbers to decide whether to include each element in the current subset or combination.

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
   - When you have multiple ways to explore (i.e., multiple branches in the decision tree), you loop to explore each of these options. For example, in **permutations**, you might loop through all elements, picking one at each recursive step, ensuring you don’t repeat elements unless specified (like in **Permutations II** with duplicates).
   
3. **Generating All Solutions**:  
   - When generating all possible solutions (e.g., in **subsets**, **combinations**, **permutations**), you loop to explore all possible subsets/choices by considering every possibility, including skipping some elements or choosing certain elements multiple times (if allowed).
   
### When **You Shouldn’t Loop**:
1. **Single Decision Point**:  
   - When you're dealing with a problem where there’s only one decision to make at each step, looping isn’t needed. For instance, in **Palindrome Partitioning**, you don't need to loop over the characters at every step because the next step is deterministic (you just need to check whether the current substring is a palindrome).
   
   ```java
   if (isPalindrome(s, start, i)) {
       tempList.add(s.substring(start, i + 1));
       backtrack(result, tempList, s, i + 1);
       tempList.remove(tempList.size() - 1);
   }
   ```
   
2. **Pruning / Early Termination**:  
   - In some cases, you might not need to loop if you have a condition that prunes the search space or eliminates paths early. For example, if you're solving a **knapsack problem** or **subset sum problem** where the sum exceeds a target value, you may not need to explore further once you've passed a certain threshold.
   - **Base cases** are often used to stop further recursion (like when a subset’s sum exceeds the target in **Combination Sum** or when the string is completely partitioned in **Palindrome Partitioning**).

3. **When You Have a Deterministic Path**:  
   - If there's only one possible solution to explore from a particular state, looping through multiple elements is unnecessary. This can happen in **constraint satisfaction problems** where the path is largely dictated by earlier choices (e.g., a Sudoku solver, where the next step is always determined based on prior steps).
   
4. **Backtracking with a Fixed Set of Choices**:  
   - In some backtracking problems like **n-queens**, you may only loop through rows or columns at a fixed position, but once the current position is fixed, there's no need to loop through other options. The backtracking decision tree itself will guide you to the next step.

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
- **Loop**: You loop over `nums` from `start` to explore all possible numbers that can be added to the current combination. This ensures that you generate all possible combinations.
- **Pruning/Stopping the Loop**: If the remaining target becomes negative, you stop the loop and return because no valid combination can be found from this point.
- **Skipping Duplicates**: If the current element is the same as the previous one (and isn't the first occurrence), you skip it to avoid generating duplicate combinations.

### Key Takeaways:
- **When to Loop**: Use a loop when you have multiple decisions to make, need to explore different choices, or need to generate all possible solutions (e.g., subsets, permutations).
- **When Not to Loop**: Avoid unnecessary looping when there is only one possible path (like in palindromes) or when the search space can be pruned early through base cases or constraints.

Hope you find this useful 😊