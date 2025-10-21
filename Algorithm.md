## Data Search Algorithms

These algorithms are used to find a specific target value within a collection of data (like an array or list).

-----

### 1\. Linear Search (Sequential Search)

  * **Explanation:** This is the simplest search method. [cite\_start]It checks each element of the data collection one by one, starting from the beginning, until the target value is found or the end of the collection is reached[cite: 1409].

  * **Sentinel Method:** A variation where the target value is temporarily added to the end of the collection (acting as a "sentinel"). [cite\_start]This simplifies the loop condition, as the search is guaranteed to find the value (either the original or the sentinel), potentially improving efficiency slightly by reducing checks within the loop[cite: 1409].

  * **Pseudocode (Basic Linear Search):**

    ```pseudocode
    // Input: Array T with N elements, Target value X
    // Output: Index I where T(I) = X, or -1 if not found

    Set I = 1
    Set Found = false

    // Loop through the array
    While I <= N AND Found = false:
        If T(I) = X:
            Set Found = true // Target found
        Else:
            Increment I by 1 // Move to the next element

    // Check if found and return result
    If Found = true:
        Return I
    Else:
        Return -1 // Target not found
    ```

  * **Pseudocode (Sentinel Method):**

    ```pseudocode
    // Input: Array T with N elements, Target value X
    // Output: Index I where T(I) = X, or -1 if not found

    // Place the sentinel
    Set OriginalValueAtEnd = T(N+1) // Store original value if needed
    Set T(N+1) = X

    Set I = 1
    // Loop until the target (or sentinel) is found
    While T(I) != X:
        Increment I by 1

    // Restore original value if needed
    Set T(N+1) = OriginalValueAtEnd

    // Check if the found element is the sentinel or the actual target
    If I <= N:
        Return I // Target found within original N elements
    Else:
        Return -1 // Target not found (only sentinel was hit)
    ```

-----

### 2\. Binary Search

  * **Explanation:** This efficient search algorithm requires the data collection to be **sorted** beforehand (e.g., in ascending order). It works by repeatedly dividing the search interval in half. It compares the target value with the middle element: if they match, the search is successful. If the target is smaller, the search continues in the lower half; if larger, it continues in the upper half. [cite\_start]This process repeats until the value is found or the interval is empty[cite: 1411].

  * **Pseudocode:**

    ```pseudocode
    // Input: Sorted Array T with N elements, Target value X
    // Output: Index M where T(M) = X, or -1 if not found

    Set L = 1 // Lower bound of search range
    Set H = N // Upper bound of search range
    Set Found = false
    Set M = -1 // Initialize M outside valid index range

    // Loop while the search range is valid and target not found
    While L <= H AND Found = false:
        Set M = integer part of (L + H) / 2 // Find middle index

        If T(M) = X:
            Set Found = true // Target found
        Else if T(M) > X:
            Set H = M - 1 // Search in the lower half
        Else: // T(M) < X
            Set L = M + 1 // Search in the upper half

    // Return result
    If Found = true:
        Return M
    Else:
        Return -1 // Target not found
    ```

-----

### 3\. Hash Search

  * **Explanation:** This method uses a **hash function** to calculate an index (or "address") directly from the target key value. This index points to the location in a hash table where the data should be stored or found. Ideally, this allows finding data in a single step. However, different keys might calculate to the same index (a "collision" or "synonym"). [cite\_start]The flowchart shows the **chaining method** to handle collisions, where items hashing to the same index are stored in a linked list starting at that index[cite: 1414, 233, 234]. [cite\_start]The search then involves calculating the index and traversing the linked list at that index if necessary[cite: 1414].

  * **Pseudocode (Using Chaining for Collisions):**

    ```pseudocode
    // Input: Hash Table HT (Array of lists/pointers), Target key X
    // Output: Data associated with key X, or "Not Found" message

    // Calculate the initial index using the hash function
    Set Index = CalculateHash(X)

    // Get the starting node of the list at the calculated index
    Set CurrentNode = HT(Index)

    // Traverse the linked list at this index
    While CurrentNode is not NULL:
        If KeyOf(CurrentNode) = X:
            Return DataOf(CurrentNode) // Target found
        Else:
            Set CurrentNode = PointerOf(CurrentNode) // Move to next node in list

    // If loop finishes without finding the key
    Return "Not Found!"
    ```

-----

## Data Sorting Algorithms

These algorithms rearrange elements in a collection (like an array) into a specific order (e.g., ascending or descending).

-----

### 1\. Selection Sort

  * **Explanation:** This algorithm divides the data into a sorted and an unsorted part. [cite\_start]It repeatedly finds the smallest (or largest) element in the unsorted part and swaps it with the first element of the unsorted part, effectively moving the boundary between sorted and unsorted parts one element forward[cite: 1417]. [cite\_start]The flowcharts show two variations: one swaps every time a smaller element is found (Fig 7-26), the other finds the minimum first and then performs a single swap per pass (Fig 7-27)[cite: 1418].

  * **Pseudocode (Finding Minimum then Swapping - like Fig 7-27):**

    ```pseudocode
    // Input: Array S with N elements
    // Output: Array S sorted in ascending order

    // Loop through the array to place each element correctly
    For I from 1 to N-1:
        Set IndexOfMin = I // Assume current element is the minimum

        // Find the index of the minimum element in the unsorted part (from I+1 to N)
        For J from I+1 to N:
            If S(J) < S(IndexOfMin):
                Set IndexOfMin = J

        // Swap the found minimum element with the first element of the unsorted part (S(I))
        If IndexOfMin != I:
            Swap S(I) and S(IndexOfMin)
    ```

-----

### 2\. Bubble Sort

  * **Explanation:** This simple sorting algorithm repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. Passes through the list are repeated until no swaps are needed, indicating the list is sorted. [cite\_start]Larger (or smaller) elements "bubble" up to their correct position[cite: 1419]. [cite\_start]The flowcharts show a basic version that reduces the comparison range by one in each pass (Fig 7-28) and an optimized version that stops early if a pass completes with no swaps (Fig 7-29)[cite: 1420].

  * **Pseudocode (Optimized - stops if no swaps, like Fig 7-29):**

    ```pseudocode
    // Input: Array S with N elements
    // Output: Array S sorted in ascending order

    Set I = 1
    Set Swapped = true // Flag to track if any swap occurred in a pass

    // Repeat passes as long as a swap occurred in the previous pass
    While Swapped = true:
        Set Swapped = false // Reset swap flag for the current pass

        // Iterate through the array, comparing adjacent elements
        For J from 1 to N-I: // Range decreases with each pass I
            If S(J) > S(J+1):
                Swap S(J) and S(J+1)
                Set Swapped = true // A swap occurred

        Increment I by 1 // Increment pass counter
    ```

-----

### 3\. Insertion Sort

  * **Explanation:** This algorithm builds the final sorted array one item at a time. [cite\_start]It iterates through the input data, taking one element at a time and inserting it into its correct position within the already sorted portion of the array[cite: 1422]. [cite\_start]To insert an element, it's compared with the elements in the sorted portion (usually from right to left) and elements are shifted right until the correct spot is found[cite: 1423].

  * **Pseudocode:**

    ```pseudocode
    // Input: Array S with N elements
    // Output: Array S sorted in ascending order

    // Start from the second element (assume first element is sorted)
    For J from 2 to N:
        Set ValueToInsert = S(J) // The element to be inserted
        Set I = J - 1 // Start comparing with the element just before it

        // Shift elements in the sorted portion (S[1..J-1]) that are greater
        // than ValueToInsert to the right
        While I > 0 AND S(I) > ValueToInsert:
            Set S(I+1) = S(I) // Shift element to the right
            Decrement I by 1

        // Insert the ValueToInsert at its correct position
        Set S(I+1) = ValueToInsert
    ```

-----

### 4\. Quick Sort

  * **Explanation:** This is an efficient, recursive sorting algorithm. It works by picking an element as a **pivot** and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively. [cite\_start]The base case for the recursion is arrays of zero or one element, which are already sorted[cite: 1425]. [cite\_start]The flowchart shows this recursive process[cite: 1426].

  * **Pseudocode (Recursive):**

    ```pseudocode
    // Main function to call the recursive sort
    Procedure QuickSort(Array S, integer N):
        Call RecursiveQuickSort(S, 1, N) // Start sorting the entire array

    // Recursive helper function
    Procedure RecursiveQuickSort(Array S, integer Left, integer Right):
        If Left < Right: // Only sort if there is more than one element
            // Choose a pivot (e.g., middle element as in the text example)
            Set PivotIndex = integer part of (Left + Right) / 2
            Set PivotValue = S(PivotIndex)

            // Partition the array around the pivot
            Set NewPivotIndex = Partition(S, Left, Right, PivotValue)

            // Recursively sort the sub-arrays
            Call RecursiveQuickSort(S, Left, NewPivotIndex - 1) // Sort left sub-array
            Call RecursiveQuickSort(S, NewPivotIndex + 1, Right) // Sort right sub-array

    // Partition function (details omitted for brevity, but it rearranges elements
    // around the pivot and returns the pivot's final index)
    Function Partition(Array S, integer Left, integer Right, integer PivotValue):
        // ... (Logic to move elements < PivotValue to the left,
        //      elements > PivotValue to the right) ...
        Return FinalIndexOfPivot
    ```

    *(Note: The actual partitioning logic can vary but the goal is to place the pivot correctly and divide the array).*

-----

## Other Algorithms

### Factorial Calculation

  * **Explanation:** The factorial of a non-negative integer N (denoted N\!) is the product of all positive integers less than or equal to N. (0\! is defined as 1). The example flowcharts show both an iterative (Fig 7-32) and a recursive (Fig 7-33) approach based on the definition N\! [cite\_start]= N \* (N-1)\![cite: 1433].

  * **Pseudocode (Recursive - like Fig 7-33):**

    ```pseudocode
    // Input: Non-negative integer N
    // Output: Factorial of N (N!)

    Function Factorial(integer N):
        If N = 0:
            Return 1 // Base case: 0! = 1
        Else:
            Return N * Factorial(N - 1) // Recursive step: N! = N * (N-1)!
    ```
