### Problem: Longest palindrome Substring
Intuition :
The obvious brute force solution is to pick all possible starting and ending positions for a substring, and verify if it is a palindrome. There are a total of n^2 such substrings (excluding the trivial solution where a character itself is a palindrome). Since verifying each substring takes O(n) time, the run time complexity is O(n^3).

Algorithm :
Pick a starting index for the current substring which is every index from 0 to n-2.
Now, pick the ending index for the current substring which is every index from i+1 to n-1.
Check if the substring from ith index to jth index is a palindrome.
If step 3 is true and length of substring is greater than maximum length so far, update maximum length and maximum substring.
Print the maximum substring.
Complexity Analysis
Time complexity : O(n^3). Assume that n is the length of the input string, there are a total of C(n, 2) = n(n-1)/2 substrings (excluding the trivial solution where a character itself is a palindrome). Since verifying each substring takes O(n) time, the run time complexity is O(n^3).

Space complexity : O(1).


### Problem: Remove Duplicates from Sorted Array
There are a few issues in your code that need to be addressed:

1. **Initial assignment to `temp[k]`**: You are assigning elements to the `temp` vector without allocating memory for it.
2. **Size of `temp`**: The `temp` vector is not initialized with any size, so you cannot directly assign elements to it at specific indices.
3. **Return value**: The size of the `temp` vector is returned, but this won't modify the original `nums` array in place, which is typically expected in problems like this.

### Explanation:
1. **Edge case**: If `nums` is empty, we return 0 right away.
2. **Unique element tracking**: The first element is always unique, so we start from index 1 (`k = 1`). Then, as we loop through the array, if an element differs from the previous one (`nums[i] != nums[i - 1]`), it is a unique element, and we store it at `nums[k]` and increment `k`.
3. **In-place modification**: This algorithm modifies the input array `nums` in place and returns the number of unique elements (`k`).

The time complexity is O(n), where n is the size of the array.


///////////////////////////////////////////////
### Problem: Container With Most Water

Given an array `height` where each element represents the height of a vertical line drawn at that index, the goal is to find two lines that, together with the x-axis, form a container that holds the most water. You need to return the maximum area of water the container can hold.

### Approach: Two Pointer Technique

- **Key Idea**: Use two pointers, one starting at the beginning (`left`) and one at the end (`right`) of the array. The area between these two lines is determined by the shorter line, as water can't rise above the shorter wall.
- **Steps**:
  1. Initialize two pointers (`left` and `right`) at the start and end of the array.
  2. Compute the area as `min(height[left], height[right]) * (right - left)`.
  3. Move the pointer pointing to the shorter line inward, as it might help in finding a taller line to maximize the area.
  4. Repeat until the two pointers meet.
### Time Complexity:
- **O(n)** where `n` is the number of elements in the `height` array (since we only loop through the array once).




///////////////////////////////////////////////////////////
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
