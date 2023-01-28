# Sorting And Search Algorithms

# Sorting with a priority queue.

- Heap Sort, Selection Sort and Insertion Sort all use the following 2 phase way of sorting
- An application of a PQ is sorting, which can be done in the following 2 steps:
    - Insertion phase: Insert the elements of sequence S as keys into an initially empty PQ by insert operations, one for each element
    - Removal phase: Call remove min on the PQ and put those elements back in the array S.
    
    (To be noted that there are 3 ways to implement a PQ)
    
    - Heap
    - Sorted List
    - Unsorted List
    
    ## Selection Sort
    
    ### Time Complexity: O (n^2)
    
    - Sorting elements using an unsorted list PQ:
        - Insertion into PQ is O(1), so n insertions give O(n) for insertion
        - the removal phase is proportional to size of PQ because for every iteration of removeMin() it has to select the minimum, so O(n)
            - which gives a total of O(n^2) complexity
    
    ### Space complexity:
    
    Depends on implementation. If the sorted sequence S is a linkedList whose size if modified by insert/remove, the total nr of elements in S and P combined is always equal to the original number in S, giving a space complexity of O(1). (doesnt scale with n)
    
    ### In-Place implementation
    
    Selection sort can be implemented in place as well:
    
    - Iterate from left to right one index i at a time
    - find index m of minimum element within i, n-1
    - swap i and m
    
    ```java
    class SelectionSort
    {
        void sort(int arr[])
        {
            int n = arr.length;
            // One by one move boundary of unsorted subarray
            for (int i = 0; i < n-1; i++)
            {
                // Find the minimum element in unsorted array
                int min_idx = i;
    	            for (int j = i+1; j < n; j++)
                    if (arr[j] < arr[min_idx])
                        min_idx = j;
     
                // Swap the found minimum element with the first
                // element
                int temp = arr[min_idx];
                arr[min_idx] = arr[i];
                arr[i] = temp;
            }
        }
     
        // Prints the array
        void printArray(int arr[])
        {
            int n = arr.length;
            for (int i=0; i<n; ++i)
                System.out.print(arr[i]+" ");
            System.out.println();
        }
     
        // Driver code to test above
        public static void main(String args[])
        {
            SelectionSort ob = new SelectionSort();
            int arr[] = {64,25,12,22,11};
            ob.sort(arr);
            System.out.println("Sorted array");
            ob.printArray(arr);
        }
    }
    ```
    
    ## Insertion Sort
    
    ### Time complexity
    
    Using a sorted List PQ:
    
    - Insertion runtime performance is proportional to size of P, giving a total of O(n^2) (n for one insertion, n*n for n insertions)
    - removal is O(n)
    
    ### Space complexity
    
    - Space complexity is the same as Selection sort.
    
    ### In-Place implementation
    
    - Insertion sort can also be done in-place, so the space complexity is always O(1).
        - Iterate left to right, one index i at a time
        - iterate backwards from i to 0, and when current element is larger then index i, shift one position to the right. When the right position is found, insert the element at i in that position.
    
    ## 
    
    ```java
    public class InsertionSort {
        /*Function to sort array using insertion sort*/
        void sort(int arr[])
        {
            int n = arr.length;
            for (int i = 1; i < n; ++i) {
                int key = arr[i];
                int j = i - 1;
     
                /* Move elements of arr[0..i-1], that are
                   greater than key, to one position ahead
                   of their current position */
                while (j >= 0 && arr[j] > key) {
                    arr[j + 1] = arr[j];
                    j = j - 1;
                }
                arr[j + 1] = key;
            }
        }
     
        /* A utility function to print array of size n*/
        static void printArray(int arr[])
        {
            int n = arr.length;
            for (int i = 0; i < n; ++i)
                System.out.print(arr[i] + " ");
     
            System.out.println();
        }
     
        // Driver method
        public static void main(String args[])
        {
            int arr[] = { 12, 11, 13, 5, 6 };
     
            InsertionSort ob = new InsertionSort();
            ob.sort(arr);
     
            printArray(arr);
        }
    };
    ```
    
    ## Heap Sort (! careful here, it s hard)
    
    ### Time complexity
    
    - the ith insert operation takes O(log i) time, since the heap has i entries after the operation. Therefore, this takes O(n log n) time ( which could be O(n) using bottom up heap construction. After this all elements are inserted in a min-heap.
    - The removal can be done with removeMin(). The j th remove operation takes O(log (n-j+1)) since the heap has n-j+1 entries. This takes O(n log n) which is the time complexity for the entire algorithm.
    
    ### Space complexity:
    
    O(n).
    
    ### In-Place:
    
    In order to achieve in-place heap sorting we need to use a portion of the array for the heap  and the remaining portion for the sorted sequence. This can be done as follows:
    
    - We use a max-heap instead of a min-heap. At any point during the execution of the algorithm, we use the left portion of S up to a certain index i - 1 to store the entries of the heap, and right to store the elements of the sequence. So, the first i elements provide the array based representation of the heap.
    - In the first phase of the algorithm, we start with an empty heap and move the boundary between the heap and the sequence to the right, and we end up with the entire array used for the heap.
    - In the second phase of the algorithm we start with an empty sequence and we move this boundary to the left again, one step at a time, by removing the maximal element from the heap and storing it at n - i.
    
    ```java
    public class HeapSort {
        public void sort(int arr[])
        {
            int N = arr.length;
     
            // Build heap (rearrange array)
            for (int i = N / 2 - 1; i >= 0; i--)
                heapify(arr, N, i);
     
            // One by one extract an element from heap
            for (int i = N - 1; i > 0; i--) {
                // Move current root to end
                int temp = arr[0];
                arr[0] = arr[i];
                arr[i] = temp;
     
                // call max heapify on the reduced heap
                heapify(arr, i, 0);
            }
        }
     
        // To heapify a subtree rooted with node i which is
        // an index in arr[]. n is size of heap
        void heapify(int arr[], int N, int i)
        {
            int largest = i; // Initialize largest as root
            int l = 2 * i + 1; // left = 2*i + 1
            int r = 2 * i + 2; // right = 2*i + 2
     
            // If left child is larger than root
            if (l < N && arr[l] > arr[largest])
                largest = l;
     
            // If right child is larger than largest so far
            if (r < N && arr[r] > arr[largest])
                largest = r;
     
            // If largest is not root
            if (largest != i) {
                int swap = arr[i];
                arr[i] = arr[largest];
                arr[largest] = swap;
     
                // Recursively heapify the affected sub-tree
                heapify(arr, N, largest);
            }
        }
     
        /* A utility function to print array of size n */
        static void printArray(int arr[])
        {
            int N = arr.length;
     
            for (int i = 0; i < N; ++i)
                System.out.print(arr[i] + " ");
            System.out.println();
        }
     
        // Driver's code
        public static void main(String args[])
        {
            int arr[] = { 12, 11, 13, 5, 6, 7 };
            int N = arr.length;
     
            // Function call
            HeapSort ob = new HeapSort();
            ob.sort(arr);
     
            System.out.println("Sorted array is");
            printArray(arr);
        }
    }
    ```
    
    # Divide and conquer
    
    It s an algorithmic design pattern consisting of 3 steps 
    
    - Divide
        - Small input: base case
        - Larger input:  recurrence case, divide the input into 2 or more disjoint sets (no common elements)
    - Conquer
        - recursively solve the sub problems associated with the subsets
    - Combine
        - take the solutions of the small problems and merge them into the solution for the larger problem
    
    # Merge sort
    
    - Merge sort uses the divide and conquer method to sort  an array of n elements
        - divide
            - if S has 0 or 1 elements it returns
            - if S has ≥ 2 elements, split these in 2 sub arrays and S1 and S2. Each contain ~ n/2 elements
        - conquer:
            - recursively sort this sub arrays S1 and S2
        - Combine:
            - Put elements back into ﻿S*S*﻿ by merging the sorted sequences into a sorted sequence (this is done by repeatedly getting the minimum of the first values of both the sorted arrays)
        
        ### Time complexity
        
        - You can visualize the algorithm using a recursive tree which contains every recursive call in a tree shape. The height h of this tree is O(log n). The overall work done at every level i is O(n) as we have to make 2^+1 recursve calls and partition and merge 2^i sequences of size n / 2 ^ i
        - Total time complexity is O (n log n)
        
        ```java
        class MergeSort {
            // Merges two subarrays of arr[].
            // First subarray is arr[l..m]
            // Second subarray is arr[m+1..r]
            public static void mergeSort(int[] s) {
                int n = s.length;
                if (n < 2)
                    return;
        
                //divide
                int mid = n / 2;
                int[] s1 = Arrays.copyOfRange(s, 0, mid);
                int[] s2 = Arrays.copyOfRange(s, mid, n);
        
                // conquer
                mergeSort(s1);
                mergeSort(s2);
        
                //merge results
                merge(s1, s2, s);
            }
        
            public static void merge(int[] s1, int[] s2, int[] s) {
                int i = 0;
                int j = 0;
                while (i + j < s.length) {
                    if (j == s2.length || (i < s1.length && s1[i] < s2[j])) {
                        s[i + j] = s1[i++];
                    } else {
                        s[i + j] = s2[j++];
                    }
                }
            }
        }
        ```
        
        ## Merge Sort in-place
        
        This is the in place version of Merge Sort.
        
        This algorithm has a time complexity of O(n*log(n)), which makes it more efficient than many other sorting algorithms for large datasets. The space complexity is O(n), since the algorithm creates two new arrays to hold the left and right halves of the original array while it sorts them.
        
        ```java
        public static void mergeSort(int[] array) {
            // base case: if the array has length 1, it is already sorted
            if (array.length > 1) {
                // split the array into two halves
                int mid = array.length / 2;
                int[] left = Arrays.copyOfRange(array, 0, mid);
                int[] right = Arrays.copyOfRange(array, mid, array.length);
        
                // sort the two halves
                mergeSort(left);
                mergeSort(right);
        
                // merge the sorted halves back together
                merge(array, left, right);
            }
        }
        
        private static void merge(int[] array, int[] left, int[] right) {
            // index for the left array
            int i = 0;
            // index for the right array
            int j = 0;
            // index for the array
            int k = 0;
        
            // while both arrays have elements remaining
            while (i < left.length && j < right.length) {
                // compare the elements at the current indices
                if (left[i] < right[j]) {
                    // the left element is smaller, so add it to the array and increment the left index
                    array[k] = left[i];
                    i++;
                } else {
                    // the right element is smaller, so add it to the array and increment the right index
                    array[k] = right[j];
                    j++;
                }
                // increment the array index
                k++;
            }
        
            // add the remaining elements from the left array to the array
            while (i < left.length) {
                array[k] = left[i];
                i++;
                k++;
            }
        
            // add the remaining elements from the right array to the array
            while (j < right.length) {
                array[k] = right[j];
                j++;
                k++;
            }
        }
        ```
        
        # Merge Sort bottom up (non recursive)
        
        ```java
        public static void mergeSort(int[] arr) {
            int n = arr.length;
            int[] temp = new int[n];
        
            for (int size = 1; size < n; size = size * 2) {
                for (int leftStart = 0; leftStart < n - 1; leftStart += 2 * size) {
                    int mid = Math.min(leftStart + size - 1, n - 1);
                    int rightEnd = Math.min(leftStart + 2 * size - 1, n - 1);
        
                    merge(arr, temp, leftStart, mid, rightEnd);
                }
            }
        }
        
        public static void merge(int[] arr, int[] temp, int leftStart, int mid, int rightEnd) {
            int leftEnd = mid;
            int rightStart = mid + 1;
            int tempIndex = leftStart;
        
            int left = leftStart;
            int right = rightStart;
        
            while (left <= leftEnd && right <= rightEnd) {
                if (arr[left] <= arr[right]) {
                    temp[tempIndex] = arr[left];
                    left++;
                } else {
                    temp[tempIndex] = arr[right];
                    right++;
                }
                tempIndex++;
            }
        
            System.arraycopy(arr, left, temp, tempIndex, leftEnd - left + 1);
            System.arraycopy(arr, right, temp, tempIndex, rightEnd - right + 1);
            System.arraycopy(temp, leftStart, arr, leftStart, rightEnd - leftStart + 1);
        }
        ```
        
        ![Untitled](Untitled%2012.png)
        
        ## QuickSort - fastest sorting algorithm they give us
        
        Quick sort uses the divide and conquer method similarly to how merge sort uses however it comes at a difference. In contrast to merge sort, most of the work is dont before the recursive calls:
        
        - Divide
            - if S has < 2 elemetns, return
            - Is S has ≥ 2 elemens, select a specifix element from s called pivot. Common practice is to chose the pivot as the last element of S. Then remove all elements of S and split them into 3 Sequences.
                - Sequence L: (left of the pivot) smaller then the pivot
                - Sequence E: (Equal to the pivot)
                - Sequence R: (right of the pivot) elements are larger than the pivot
        - Conquer
            - Recursively sort L and R
        - Combine
            - Put elements back into S: first all elements of L then of E and then of R
        
        ### Time Complexity:
        
        - Running time is the same as merge sort, O (n log n ) and space is log n but since the pivot selection is randomized and with a bit of statistics it can be faster then merge sort classical
            - If the pivot is always the worst choice (smallest or biggest elemetn) then complexity is O(n^2 ) because the height becomes O(n)
                - And O (n) space
            
            ```java
            public static void quickSort(int[] arr) {
                quickSort(arr, 0, arr.length - 1);
            }
            
            private static void quickSort(int[] arr, int low, int high) {
                if (low < high) {
                    int pivotIndex = partition(arr, low, high);
                    quickSort(arr, low, pivotIndex);
                    quickSort(arr, pivotIndex + 1, high);
                }
            }
            
            private static int partition(int[] arr, int low, int high) {
                int pivot = arr[high];
                int i = low - 1;
                for (int j = low; j < high; j++) {
                    if (arr[j] <= pivot) {
                        i++;
                        int temp = arr[i];
                        arr[i] = arr[j];
                        arr[j] = temp;
                    }
                }
                int temp = arr[i + 1];
                arr[i + 1] = arr[high];
                arr[high] = temp;
                return i + 1;
            }
            ```
            
        
        ### Randomized quick sort
        
        The pivot is randomly chosen! (there s a lot of stats and maths involved in the why is this faster)
        
        ### In place quick sort
        
        A sub sequence of the input is represented implicitly by the range given by indexes a and b. The following changes must be made
        
        - Select the last item in the current list as picot
        - the divide step scans the arrays simultaneously
            - forward using l
            - backwards using r
            - if an item with index r is lower than pivot, then r was in the right place.
        - When indexes cross, division is complete and the alg. recurs on the 2 sub-sequences. No explicit combine step is needed. We now also dont create 3 sequences, 3 values equal to the pivot point can be dispersed across the sub - lists.
        
        The time complexity of the non-in-place quicksort algorithm I provided is the same as the in-place version, which is O(n*log(n)) on average, but can be as bad as O(n^2) in the worst case.
        
        However, the space complexity is different. While the in-place version has a space complexity of O(log(n)), since it creates a new call stack for each level of recursion, the non-in-place version has a space complexity of O(n). This is because it creates new arrays to hold the left and right halves of the original array while it sorts them, and then combines them back into a single array at the end.
        
        ## Quick Sort in-place
        
        This version of the quicksort algorithm is in-place, meaning it sorts the elements of the original array without creating any new arrays. This makes it more memory efficient than the non-in-place version, but it does not return the sorted array as a result.
        
        The time complexity of this algorithm is the same as the in-place version of quicksort that I provided earlier, which is O(n*log(n)) on average, but can be as bad as O(n^2) in the worst case. The space complexity is O(log(n)), since the algorithm creates a new call stack for each level of recursion.
        
        ```java
        public static void quickSort(int[] array, int left, int right) {
            // base case: if the left index is greater than or equal to the right index, the array is already sorted
            if (left < right) {
                // partition the array around a pivot element
                int pivotIndex = partition(array, left, right);
        
                // sort the left and right halves of the array
                quickSort(array, left, pivotIndex - 1);
                quickSort(array, pivotIndex + 1, right);
            }
        }
        
        private static int partition(int[] array, int left, int right) {
            // choose the rightmost element as the pivot
            int pivot = array[right];
            // index of the first element greater than the pivot
            int i = left;
        
            // loop through the array and move elements that are less than the pivot to the left side
            for (int j = left; j < right; j++) {
                if (array[j] < pivot) {
                    // swap the element at index i with the element at index j
                    int temp = array[i];
                    array[i] = array[j];
                    array[j] = temp;
                    // increment i to move on to the next element
                    i++;
                }
            }
        
            // swap the pivot element into its final position
            array[right] = array[i];
            array[i] = pivot;
        
            return i;
        }
        ```
        
        ## Quick Select algorithm
        
        QuickSelect is an algorithm that selects the k th smallest element from an input sequence S.(you can also do this with a Heap and remove k elements  from it but this is faster)
        
        Prune-and-search method
        
        - Prune away a fraction of n elements
        - Recursively solve the smaaller problem
        - find solution for best case using brute force
        
        Very similar to binary search but the pivot is random. 
        
        - As for the time and space complexity of quick select, the worst case time complexity is O(n^2) and the worst case space complexity is O(n). This occurs when the pivot is always the smallest or largest element in the array, causing the algorithm to degrade to selection sort. However, the average case time complexity is O(n), making it more efficient than quicksort in practice. The space complexity is constant, O(1), as the algorithm does not use any additional space.
        
        ```java
        import java.util.Random;
        
        public class QuickSelect {
          public static int quickSelect(int[] arr, int k) {
            return quickSelect(arr, 0, arr.length - 1, k - 1);
          }
        
          private static int quickSelect(int[] arr, int left, 
        																	int right, int k) {
            // Generate a random pivot index
            Random random = new Random();
            int pivotIndex = left + random.nextInt(right - left + 1);
        
            // Partition the array around the pivot
            pivotIndex = partition(arr, left, right, pivotIndex);
        
            // Return the kth element if it is the pivot
            if (k == pivotIndex) {
              return arr[k];
            }
            // Recursively search the left or right half of the array
            else if (k < pivotIndex) {
              return quickSelect(arr, left, pivotIndex - 1, k);
            } else {
              return quickSelect(arr, pivotIndex + 1, right, k);
            }
          }
        
          private static int partition(int[] arr, int left, int right, 
        																int pivotIndex) {
            int pivotValue = arr[pivotIndex];
            swap(arr, pivotIndex, right);
            int storeIndex = left;
            for (int i = left; i < right; i++) {
              if (arr[i] < pivotValue) {
                swap(arr, storeIndex, i);
                storeIndex++;
              }
            }
            swap(arr, right, storeIndex);
            return storeIndex;
          }
        
          private static void swap(int[] arr, int i, int j) {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
          }
        }
        ```
        
        ![Untitled](Untitled%2013.png)
        
        ## Bubble Sort algorithm
        
        Complexity is O(n^2)
        
        ```java
        public static void bubbleSort(int[] array) {
          boolean sorted = false;
          int n = array.length;
          while (!sorted) {
              sorted = true;
              for (int i = 1; i < n; i++) {
                  if (array[i - 1] > array[i]) {
                      sorted = false;
                      int temp = array[i - 1];
                      array[i - 1] = array[i];
                      array[i] = temp;
                  }
              }
              n--;
          }
        }
        ```
        
        ## 2 for sorting
        
        O(n^2)
        
        ```java
        public static void selectionSort(int[] array) {
          for (int i = 0; i < array.length - 1; i++) {
              int minIndex = i;
              for (int j = i + 1; j < array.length; j++) {
                  if (array[j] < array[minIndex]) {
                      minIndex = j;
                  }
              }
              int temp = array[i];
              array[i] = array[minIndex];
              array[minIndex] = temp;
          }
        }
        ```
        
        ## Binary Search
        
        O (n log n)
        
        ```java
        public class BinarySearch {
        
            public static int binarySearch(int[] arr, int target) {
                int left = 0;
                int right = arr.length - 1;
                while (left <= right) {
                    int mid = left + (right - left) / 2;
                    if (arr[mid] == target) {
                        return mid;
                    } else if (arr[mid] < target) {
                        left = mid + 1;
                    } else {
                        right = mid - 1;
                    }
                }
                return -1;
            }
        }
        ```
        
        ## Bucket Sort
        
        Time and space is O (n + N) where N is number of buckets and n is nr of elements in the array. It is a stable sorting algorithm.
        
        ```java
        import java.util.ArrayList;
        import java.util.Collections;
        
        public class BucketSort {
        
          public static void sort(int[] arr) {
            int maxVal = getMax(arr);
        
            // Create buckets
            ArrayList<ArrayList<Integer>> buckets = new ArrayList<ArrayList<Integer>>(maxVal + 1);
            for (int i = 0; i < buckets.size(); i++) {
              buckets.add(new ArrayList<Integer>());
            }
        
            // Distribute input array values into buckets
            for (int i : arr) {
              buckets.get(i).add(i);
            }
        
            // place it back into the input array
            int currentIndex = 0;
            for (ArrayList<Integer> bucket : buckets) {
              for (int i : bucket) {
                arr[currentIndex++] = i;
              }
            }
          }
        
          private static int getMax(int[] arr) {
            int max = arr[0];
            for (int i = 1; i < arr.length; i++) {
              if (arr[i] > max) {
                max = arr[i];
              }
            }
            return max;
          }
        }
        ```
        
    
    # Radix Sort
    
    It s applying bucketSort for every element in the key of sorting. It can be done LSD (least significant digit first) or MSD (most significant digit first)
    
    ## LSD using the above bucketSort
    
    This implementation of LSD radix sort works by sorting the input array based on each character, starting with the least significant character and working towards the most significant character. It uses the bucket sort algorithm to sort the elements within each bucket. The time complexity of this implementation is O(d(n + b)), where d is the length of the longest string, n is the size of the input array, and b is the number of buckets.
    
    ```java
    import java.util.ArrayList;
    import java.util.Collections;
    
    public class LSDRadixSort {
    
      public static void sort(ArrayList<String> arr, int stringLength) {
        for (int i = stringLength - 1; i >= 0; i--) {
          sortByCharacter(arr, i);
        }
      }
    
      private static void sortByCharacter(ArrayList<String> arr, int characterIndex) {
        // Create buckets
        ArrayList<String>[] buckets = new ArrayList[27];
        for (int i = 0; i < buckets.length; i++) {
          buckets[i] = new ArrayList<String>();
        }
    
        // Distribute input array values into buckets based on the current character
        for (String s : arr) {
          char c = s.charAt(characterIndex);
          int index = (c == ' ') ? 0 : c - 'a' + 1;
          buckets[index].add(s);
        }
    
        // Sort each bucket and place it back into the input array
        int currentIndex = 0;
        for (ArrayList<String> bucket : buckets) {
          BucketSort.sort(bucket);
          for (String s : bucket) {
            arr.set(currentIndex++, s);
          }
        }
      }
    
      private static class BucketSort {
    
        public static void sort(ArrayList<String> arr) {
          // Find the maximum value in the input array
          int maxVal = Integer.MIN_VALUE;
          for (String s : arr) {
            maxVal = Math.max(maxVal, s.length());
          }
    
          // Create buckets
          ArrayList<ArrayList<String>> buckets = new ArrayList<ArrayList<String>>(maxVal + 1);
          for (int i = 0; i < buckets.size(); i++) {
            buckets.add(new ArrayList<String>());
          }
    
          // Distribute input array values into buckets
          for (String s : arr) {
            buckets.get(s.length()).add(s);
          }
    
          // Sort each bucket and place it back into the input array
          int currentIndex = 0;
          for (ArrayList<String> bucket : buckets) {
            Collections.sort(bucket);
            for (String s : bucket) {
              arr.set(currentIndex++, s);
            }
          }
        }
      }
    }
    ```
    
    ## MSD
    
    This implementation of MSD radix sort works by recursively sorting the input array based on each character, starting with the most significant character and working towards the least significant character. It uses the bucket sort algorithm to sort the elements within each bucket. The time complexity of this implementation is O(d(n + b)), where d is the length of the longest string, n is the size of the input array, and b is the number of buckets.
    
    ```java
    import java.util.ArrayList;
    import java.util.Collections;
    
    public class MSDRadixSort {
    
      public static void sort(ArrayList<String> arr) {
        sort(arr, 0, arr.size() - 1, 0);
      }
    
      private static void sort(ArrayList<String> arr, int low, int high, int characterIndex) {
        if (low >= high) {
          return;
        }
    
        // Create buckets
        ArrayList<String>[] buckets = new ArrayList[27];
        for (int i = 0; i < buckets.length; i++) {
          buckets[i] = new ArrayList<String>();
        }
    
        // Distribute input array values into buckets based on the current character
        for (int i = low; i <= high; i++) {
          String s = arr.get(i);
          char c = (characterIndex >= s.length()) ? ' ' : s.charAt(characterIndex);
          int index = (c == ' ') ? 0 : c - 'a' + 1;
          buckets[index].add(s);
        }
    
        // Recursively sort each bucket
        int currentIndex = low;
        for (int i = 0; i < buckets.length; i++) {
          ArrayList<String> bucket = buckets[i];
          if (bucket.size() > 1) {
            sort(bucket, 0, bucket.size() - 1, characterIndex + 1);
          }
          for (String s : bucket) {
            arr.set(currentIndex++, s);
          }
        }
      }
    }
    ```
    
    ![Untitled](Untitled%2014.png)