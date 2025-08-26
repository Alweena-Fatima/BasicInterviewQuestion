# Bubble Sort

### Steps
1. Traverse the array from the beginning.  
2. Compare adjacent elements:  
   - If the current element is greater than the next (for ascending order), swap them.  
1. After one full pass, the largest element “bubbles up” to its correct position at the end of the array.  
2. Repeat the passes for the remaining unsorted part of the array.  
3. Stop when a pass requires no swaps, meaning the array is sorted.
### Time Complexity
- Worst Case: O(N²) → Array in reverse order  
- Best Case: O(N) → Array already sorted (with optimized swap check)  
- Average Case: O(N²)  
### Space Complexity
- O(1) → In-place sorting

### Observations
- After each pass, at least one element reaches its correct position.
- Simple to implement but inefficient for large datasets.


```java
public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;
        // Traverse the array multiple times
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            // Compare adjacent elements(n-1-i) - beacuse after every i last element will be at correct postion so we dont need to compare it 
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap if elements are in wrong order
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            // If no swaps in this pass, array is sorted
            if (!swapped) break;
        }
}
```

# Selection Sort (Concept)

- **Idea:** Divide the array into **sorted** and **unsorted** parts.
- **Steps:**
  1. Initially, the **sorted part** is empty and the **unsorted part** is the whole array.
  2. **Iterate through the unsorted part** to find the **minimum element**.
  3. **Swap** this minimum element with the **first element** of the unsorted part.
  4. **Expand the sorted part** by moving the boundary one step to the right.
  5. Repeat until the **unsorted part is empty** and the array is fully sorted.

- **Key Observations:**
  - Reduces the number of swaps compared to Bubble Sort.
  - Time Complexity: O(N²) in all cases.
  - Space Complexity: O(1) (in-place).
  - Not stable (equal elements may change relative order).
```java
public static void selectionSort(int[] arr) {
        int n = arr.length;
        // Move the boundary of the sorted part
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            // Find the minimum element in the unsorted part
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            // Swap the found minimum with the first element of the unsorted part (i will be the first index of unsorted part left to i is sorted )
            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }
    }
}
```
---

# Insertion Sort (Concept)

- **Idea:** Divide the array into **sorted** and **unsorted** parts.  
- **Steps:**
  1. Initially, the sorted part contains the first element, and the unsorted part is the rest of the array.  
  2. Take the first element of the unsorted part.  
  3. Find the correct position for it in the sorted part by shifting larger elements to the right.  
  4. Insert the element at its correct position in the sorted part.  
  5. Expand the sorted part by including this newly inserted element.  
  6. Repeat until the unsorted part is empty and the array is fully sorted.

- **Key Points:**
  - Efficient for **small or nearly sorted arrays**.
  - **Stable sorting algorithm** (preserves relative order of equal elements).  
  - Time Complexity:  
    - Best Case (already sorted): O(N)  
    - Worst/Average Case: O(N²)  
  - Space Complexity: O(1) → in-place.
```java
public static void insertionSort(int[] arr) {
        int n = arr.length;
        // Iterate over the unsorted part
        for (int i = 1; i < n; i++) {
            int key = arr[i]; // element to insert(first elemnt of unsorted)
            int j = i - 1;
            // Shift elements of sorted part greater than key to the right
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            // Insert key at correct position in sorted part
            arr[j + 1] = key;
        }
    }
```
# Merge Sort

### Idea
- **Divide and Conquer** algorithm.
- **Steps:**
  1. **Divide** the unsorted array into two halves.
  2. Recursively **divide each half** until each sublist contains **a single element** (which is trivially sorted).
  3. **Merge** the sublists by comparing elements and forming a **sorted list**.
  4. Repeat merging until the entire array is merged and sorted.

### Key Points
- Uses **recursion**.
- Stable sorting algorithm (preserves order of equal elements).
- Time Complexity:
  - Best / Worst / Average Case: O(N log N)
- Space Complexity: O(N) → requires temporary arrays for merging.
- Efficient for large datasets compared to Bubble, Insertion, or Selection Sort.

```java
// Merge Sort in Java
public class MergeSort {
    // Recursive merge sort function (this function will divide the array until it has single element When `left == right`, the subarray has **a single element**, so it’s already sorted and recursion stops.)
    public static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            // Divide left half
            mergeSort(arr, left, mid);
            // Divide right half
            mergeSort(arr, mid + 1, right);
            // Merge sorted halves
            merge(arr, left, mid, right);
        }
    }

    // Merge two sorted subarrays (this will get two array arr1 - left to mid and arr2 - mid+1 to right)
    public static void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        int[] L = new int[n1];
        int[] R = new int[n2];
        for (int i = 0; i < n1; i++) L[i] = arr[left + i];
        for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];
        int i = 0, j = 0, k = left;// i for L and j for R traversal
        // Merge the two arrays
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }
        // Copy remaining elements
        while (i < n1) arr[k++] = L[i++];
        while (j < n2) arr[k++] = R[j++];
    }
    public static void main(String[] args) {
        int[] arr = {38, 27, 43, 3, 9, 82, 10};
        mergeSort(arr, 0, arr.length - 1);
    }
}
```
---
# Quick Sort

### Idea
- Divide and Conquer algorithm.
- Steps:
  1. Choose a pivot element (first, last, middle, or random).
  2. Partition the array:
     - Elements less than pivot → left subarray.
     - Elements greater than pivot → right subarray.
     - Pivot is in its correct sorted position.
  3. Recursively apply Quick Sort to left and right subarrays.
  4. Stop when subarray has 0 or 1 element.

### Key Points
- Uses recursion.
- In-place sorting (no extra arrays needed like Merge Sort).
- Not stable (equal elements may change order).
- Time Complexity:
  - Best / Average Case: O(N log N)
  - Worst Case: O(N²) → occurs with bad pivot choice.
- Space Complexity: O(log N) → recursion stack.
- Efficient for large datasets.
```java
public class QuickSort {
    // Partition function
    static int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; // choose pivot
        int i = low - 1; // index of smaller element  
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        // swap arr[i+1] and pivot
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;
        
        return i + 1; // return pivot position
    }
    // QuickSort function
    static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);   // sort left
            quickSort(arr, pi + 1, high);  // sort right
        }
    }
    // Main function to test
    public static void main(String[] args) {
        int[] arr = {8, 4, 7, 9, 3, 5};
        quickSort(arr, 0, arr.length - 1);
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---
# Heap Sort

### Idea
- Comparison-based sorting algorithm based on Binary Heap.
- Steps:
  1. Build a Max Heap from the array.
  2. Swap the root (largest element) with the last element.  
     - Now the root is in its correct sorted position.
  3. Reduce heap size by 1 (ignore the last element as it's sorted).
  4. Heapify the root to restore Max Heap property.
  5. Repeat steps 2–4 until the heap size becomes 1.

### Key Points
- Uses heap data structure.
- In-place sorting (no extra array needed).
- Not stable (relative order of equal elements may change).
- Time Complexity:
  - Best / Average / Worst Case: O(N log N)
- Space Complexity: O(1) → in-place
- Efficient for large datasets.

```java
public class HeapSort {
    static void heapify(int[] arr, int n, int i) {
    //here i is parent it will cheack if parent is greater then both child or not if not then swap 
        int largest = i; // parent
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        if (left < n && arr[left] > arr[largest]) largest = left;
        if (right < n && arr[right] > arr[largest]) largest = right;
        if (largest != i) {
            int temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;
            heapify(arr, n, largest); // recursively heapify
        }
    }
    static void heapSort(int[] arr) {
        int n = arr.length;
        // Build max heap(leaf node doesnt have chlid to heapify islie n/2)
        for (int i = n / 2 - 1; i >= 0; i--) heapify(arr, n, i);
        // Extract elements from heap(swap root with last element)
        for (int i = n - 1; i > 0; i--) {
            // Move current root to end
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            // Heapify reduced heap
            heapify(arr, i, 0);
        }
    }
    public static void main(String[] args) {
        int[] arr = {8, 4, 7, 9, 3, 5};
        heapSort(arr);
        for (int num : arr) System.out.print(num + " ");
    }
}
```
