### **Median of the Two Sorted Arrays**
This code defines a C++ class `Solution` with a method `findMedianSortedArrays` that finds the median of two sorted arrays `nums1` and `nums2`. Here's a breakdown of how the code works:

### **Overview:**
The method merges the two sorted arrays while keeping track of the middle element (or elements) to calculate the median efficiently. It uses two pointers to traverse both arrays simultaneously and merges them in sorted order without explicitly creating a merged array.

### **Step-by-step Explanation:**

1. **Initial Setup:**
    ```cpp
    int m = nums1.size();
    int n = nums2.size();
    int total = m + n;
    int mid = total / 2;
    ```
   - `m` and `n` store the sizes of `nums1` and `nums2` respectively.
   - `total` is the sum of the lengths of both arrays (i.e., the total number of elements).
   - `mid` is the index of the middle element in the merged array.

2. **Two-Pointer Merge:**
    ```cpp
    int i = 0, j = 0;
    int prev = 0, curr = 0;
    ```
   - `i` and `j` are pointers that iterate through `nums1` and `nums2` respectively.
   - `prev` and `curr` are variables used to track the last two elements in the merged sequence, which are essential for calculating the median.

3. **Merging Process:**
    ```cpp
    for (int count = 0; count <= mid; count++) {
        prev = curr;
        if (i < m && (j >= n || nums1[i] <= nums2[j])) {
            curr = nums1[i++];
        } else {
            curr = nums2[j++];
        }
    }
    ```
   - The loop runs until it reaches the middle of the merged array (`mid` index).
   - At each iteration, it updates `prev` to the value of `curr`.
   - It selects the smaller element from the two arrays (pointed to by `i` and `j`) to be the next element in the merged sequence (`curr`).
   - If all elements in `nums2` have been used (`j >= n`), or the current element in `nums1` is smaller (`nums1[i] <= nums2[j]`), it increments the `i` pointer; otherwise, it increments the `j` pointer.

4. **Median Calculation:**
    ```cpp
    if (total % 2 == 1) {
        return curr;
    }
    return (prev + curr) / 2.0;
    ```
   - If the total number of elements is odd, the median is the current middle element (`curr`).
   - If the total number of elements is even, the median is the average of the last two elements in the merged sequence (`prev` and `curr`).

### **Example:**

If `nums1 = [1, 3]` and `nums2 = [2]`:

- The merged array would be `[1, 2, 3]`.
- The total number of elements is 3 (odd), so the median is `2`, the middle element.

If `nums1 = [1, 2]` and `nums2 = [3, 4]`:

- The merged array would be `[1, 2, 3, 4]`.
- The total number of elements is 4 (even), so the median is the average of `2` and `3`, which is `2.5`.

### **Time Complexity:**

The time complexity of this approach is **O(m + n)**, where `m` and `n` are the lengths of the two arrays. This is because we are essentially merging the two arrays by iterating through them linearly until we reach the middle.

### **Space Complexity:**

The space complexity is **O(1)** since no additional data structures are used beyond a few variables to store indices and values.
