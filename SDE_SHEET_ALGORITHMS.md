# STRIVER'S SDE SHEET — COMPLETE ALGORITHM CHEATSHEET
### Amazon SDE2 Interview Revision

---

## TABLE OF CONTENTS
1. [Arrays (24 problems)](#arrays)
2. [Linked List (18 problems)](#linked-list)
3. [Greedy (6 problems)](#greedy)
4. [Recursion & Backtracking (12 problems)](#recursion--backtracking)
5. [Binary Search (8 problems)](#binary-search)
6. [Stack & Queue (12 problems)](#stack--queue)
7. [Strings (10 problems)](#strings)
8. [Binary Tree (27 problems)](#binary-tree)
9. [BST (14 problems)](#bst)
10. [Graph (18 problems)](#graph)
11. [Dynamic Programming (14 problems)](#dynamic-programming)
12. [Heaps (6 problems)](#heaps)
13. [Trie (7 problems)](#trie)

---

# ARRAYS

## DAY 1

### 1. Set Matrix Zeroes
**TC:** O(M*N) | **SC:** O(1)

1. Use first row and first column as markers. Use two boolean flags `row0`, `col0` to track if row 0 or col 0 themselves need to be zeroed.
2. Scan entire matrix. If `matrix[i][j] == 0`, set `matrix[i][0] = 0` and `matrix[0][j] = 0`.
3. Process inner matrix (rows 1..M-1, cols 1..N-1): if `matrix[i][0] == 0` OR `matrix[0][j] == 0`, set `matrix[i][j] = 0`.
4. If `col0` flag true, zero out entire column 0. If `row0` flag true, zero out entire row 0.

---

### 2. Pascal's Triangle
**TC:** O(N^2) | **SC:** O(N^2)

1. Initialize result with first row `[1]`.
2. For each new row i from 1 to N-1: start with `[1]`, for each position j from 1 to i-1 append `prev[j-1] + prev[j]`, end with `[1]`.
3. Append row to result.

---

### 3. Next Permutation
**TC:** O(N) | **SC:** O(1)

1. Find the rightmost index `i` where `nums[i] < nums[i+1]`. If none, go to step 4.
2. Find the rightmost index `j > i` where `nums[j] > nums[i]`.
3. Swap `nums[i]` and `nums[j]`.
4. Reverse the suffix starting at `i+1` (or entire array if step 1 found nothing).

---

### 4. Kadane's Algorithm (Maximum Subarray Sum)
**TC:** O(N) | **SC:** O(1)

1. Initialize `maxSum = INT_MIN`, `currentSum = 0`.
2. For each element: `currentSum += nums[i]`. Update `maxSum = max(maxSum, currentSum)`.
3. If `currentSum < 0`, reset `currentSum = 0`.
4. Return `maxSum`.

---

### 5. Sort 0s, 1s, 2s (Dutch National Flag)
**TC:** O(N) | **SC:** O(1)

1. Initialize three pointers: `low = 0`, `mid = 0`, `high = N-1`.
2. While `mid <= high`:
   - If `nums[mid] == 0`: swap `nums[low]` and `nums[mid]`, `low++`, `mid++`.
   - If `nums[mid] == 1`: `mid++`.
   - If `nums[mid] == 2`: swap `nums[mid]` and `nums[high]`, `high--`. (**Do NOT increment mid.**)

---

### 6. Best Time to Buy and Sell Stock
**TC:** O(N) | **SC:** O(1)

1. Initialize `minPrice = prices[0]`, `maxProfit = 0`.
2. For each price: `minPrice = min(minPrice, price)`. `maxProfit = max(maxProfit, price - minPrice)`.
3. Return `maxProfit`.

---

## DAY 2

### 7. Rotate Image (90° clockwise)
**TC:** O(N^2) | **SC:** O(1)

1. Transpose the matrix: swap `matrix[i][j]` with `matrix[j][i]` for all `i < j`.
2. Reverse each row.
- **Anti-clockwise:** Reverse each column first, then transpose.

---

### 8. Merge Intervals
**TC:** O(N log N) | **SC:** O(N)

1. Sort intervals by start time.
2. Initialize result with first interval.
3. For each subsequent interval:
   - If `interval.start <= result.last.end`: merge by updating `result.last.end = max(result.last.end, interval.end)`.
   - Else: append interval to result.
4. Return result.

---

### 9. Merge Two Sorted Arrays Without Extra Space
**TC:** O((M+N) log(M+N)) | **SC:** O(1)

**Gap Method:**
1. Compute initial `gap = ceil((M+N)/2)`.
2. While `gap > 0`: compare and swap elements that are `gap` apart across both arrays if out of order.
3. Reduce `gap = ceil(gap/2)`. If gap was 1, set to 0 and stop.

**Simpler Swap+Sort approach:** O(n log n + m log m)
1. `i = n-1` (end of arr1), `j = 0` (start of arr2).
2. While `i >= 0 and j < m`: if `arr1[i] > arr2[j]`, swap, `i--`, `j++`. Else break.
3. Sort arr1 and arr2 separately.

---

### 10. Find Duplicate Number
**TC:** O(N) | **SC:** O(1)

**Floyd's Cycle Detection:**
1. Phase 1: `slow = nums[0]`, `fast = nums[nums[0]]`. While `slow != fast`: `slow = nums[slow]`, `fast = nums[nums[fast]]`.
2. Phase 2: Reset `slow = nums[0]`. While `slow != fast`: `slow = nums[slow]`, `fast = nums[fast]`.
3. Return `slow` (meeting point = duplicate).

---

### 11. Repeat and Missing Number
**TC:** O(N) | **SC:** O(1)

1. Find duplicate using Floyd's Cycle Detection (Problem 10).
2. Compute `actualSum = sum of array`. `expectedSum = N*(N+1)/2`.
3. `missing = expectedSum - (actualSum - duplicate)`.
4. Return `[duplicate, missing]`.

---

### 12. Count Inversions
**TC:** O(N log N) | **SC:** O(N)

**Modified Merge Sort:**
1. Divide array into halves recursively until single elements.
2. During merge: when `right[j] < left[i]`, all elements from `i to mid` form inversions with `right[j]`. Add `(mid - i + 1)` to count.
3. Merge normally (sorted order). Sum counts from all levels.

---

## DAY 3

### 13. Search in 2D Matrix
**TC:** O(log(M*N)) | **SC:** O(1)

**Fully sorted matrix (each row's first > prev row's last):**
1. Treat as 1D array. Binary search: `mid_val = matrix[mid/N][mid%N]`.
2. Standard binary search logic.

**Row-wise + column-wise sorted:**
1. Start at top-right: `row=0`, `col=N-1`.
2. If `matrix[row][col] == target`: return true. If `> target`: `col--`. If `< target`: `row++`.

---

### 14. Pow(x, n)
**TC:** O(log N) | **SC:** O(1) iterative

**Iterative Fast Exponentiation:**
1. If `n < 0`: `x = 1/x`, `n = -n`.
2. `result = 1`. While `n > 0`: if `n is odd`, `result *= x`. `x *= x`, `n /= 2`.
3. Return `result`.

---

### 15. Majority Element (> N/3 times)
**TC:** O(N) | **SC:** O(1)

**Extended Boyer-Moore Voting:**
1. Maintain two candidates `c1`, `c2` with `cnt1=0`, `cnt2=0`.
2. For each element: if equals c1, cnt1++; else if equals c2, cnt2++; else if cnt1==0, c1=element, cnt1=1; else if cnt2==0, c2=element, cnt2=1; else cnt1--, cnt2--.
3. Verify both candidates by counting actual occurrences. Return those exceeding N/3.

---

### 16. Majority Element (> N/2 times)
**TC:** O(N) | **SC:** O(1)

**Boyer-Moore Voting:**
1. `candidate = nums[0]`, `count = 1`.
2. For each subsequent element: if equals candidate, count++; else count--. If count==0, candidate = current, count=1.
3. Return candidate (verify if not guaranteed to exist).

---

### 17. Grid Unique Paths
**TC:** O(M*N) | **SC:** O(N) (space optimized)

1. `dp[M][N]` where `dp[i][j]` = paths to (i,j). Set first row and column to 1.
2. For i from 1, j from 1: `dp[i][j] = dp[i-1][j] + dp[i][j-1]`.
3. Return `dp[M-1][N-1]`.
- **Math shortcut:** Answer = C(M+N-2, M-1).

---

### 18. Reverse Pairs (nums[i] > 2*nums[j], i < j)
**TC:** O(N log N) | **SC:** O(N)

**Modified Merge Sort:**
1. During merge of left and right halves (both sorted): count pairs using two-pointer where `left[i] > 2*right[j]`.
2. For each i in left, find all j in right satisfying condition. Advance j as needed.
3. Then perform normal merge. Sum counts from all recursive levels.

---

## DAY 4

### 19. Two Sum
**TC:** O(N) | **SC:** O(N)

1. HashMap stores `{value -> index}`.
2. For each element: check if `target - nums[i]` in map. If yes, return indices. Else put `nums[i]` in map.

---

### 20. 4 Sum
**TC:** O(N^3) | **SC:** O(1)

1. Sort the array.
2. Fix `i` (0 to N-4), skip duplicates. Fix `j` (i+1 to N-3), skip duplicates.
3. Two pointers `left=j+1`, `right=N-1`. If sum==target: record, skip duplicates, left++, right--. If sum<target: left++. If sum>target: right--.

---

### 21. Longest Consecutive Sequence
**TC:** O(N) | **SC:** O(N)

1. Put all elements in HashSet.
2. For each `num`: only start counting if `num-1` NOT in set (sequence start).
3. Expand: while `num+1` in set, length++. Update maxLength.

---

### 22. Largest Subarray with Sum 0
**TC:** O(N) | **SC:** O(N)

1. HashMap stores first occurrence of prefix sum: `{0: -1}`.
2. For each i: `prefixSum += nums[i]`. If prefixSum in map: `length = i - map[prefixSum]`, update maxLength. Else store `map[prefixSum] = i`.

---

### 23. Count Subarrays with XOR = K
**TC:** O(N) | **SC:** O(N)

1. HashMap for prefix XOR frequencies: `{0: 1}`.
2. For each element: `xorSum ^= nums[i]`. If `xorSum ^ K` in map, add its count to answer.
3. Increment `map[xorSum]`.

---

### 24. Longest Substring Without Repeating Characters
**TC:** O(N) | **SC:** O(min(M,N))

1. Sliding window. HashMap: char -> last seen index. `left=0`, `maxLen=0`.
2. For each `right`: if char seen and `lastIndex >= left`, move `left = lastIndex + 1`.
3. Update `lastIndex[char] = right`. `maxLen = max(maxLen, right - left + 1)`.

---

# LINKED LIST

## DAY 5

### 25. Reverse Linked List
**TC:** O(N) | **SC:** O(1)

1. `prev=null`, `curr=head`.
2. While `curr != null`: save `next=curr.next`, `curr.next=prev`, `prev=curr`, `curr=next`.
3. Return `prev`.

---

### 26. Find Middle of Linked List
**TC:** O(N) | **SC:** O(1)

1. `slow=head`, `fast=head`.
2. While `fast != null && fast.next != null`: `slow=slow.next`, `fast=fast.next.next`.
3. Return `slow`.

---

### 27. Merge Two Sorted Lists
**TC:** O(M+N) | **SC:** O(1)

1. Dummy node, `curr=dummy`.
2. While both non-null: append smaller node, advance that pointer.
3. Attach remaining list. Return `dummy.next`.

---

### 28. Remove Nth Node from End
**TC:** O(N) | **SC:** O(1)

1. Dummy node pointing to head.
2. Advance `fast` N+1 steps from dummy.
3. Move both `slow` (from dummy) and `fast` until fast is null.
4. `slow.next = slow.next.next`. Return `dummy.next`.

---

### 29. Delete Given Node (no head given)
**TC:** O(1) | **SC:** O(1)

1. Copy next node's value: `node.val = node.next.val`.
2. Skip next node: `node.next = node.next.next`.

---

### 30. Add Two Numbers as Linked Lists
**TC:** O(max(M,N)) | **SC:** O(max(M,N))

1. Dummy head, `carry=0`, `curr=dummy`.
2. While `l1 != null OR l2 != null OR carry != 0`: `sum = l1.val + l2.val + carry`. Create node with `sum % 10`, `carry = sum / 10`. Advance l1, l2 if non-null.
3. Return `dummy.next`.

---

## DAY 6

### 31. Intersection of Two Linked Lists
**TC:** O(M+N) | **SC:** O(1)

1. `a=headA`, `b=headB`.
2. While `a != b`: advance each; when one reaches null, redirect to other list's head.
3. They meet at intersection (or both null = no intersection).

---

### 32. Detect Cycle in Linked List
**TC:** O(N) | **SC:** O(1)

1. `slow=head`, `fast=head`.
2. While `fast != null && fast.next != null`: `slow=slow.next`, `fast=fast.next.next`.
3. If `slow == fast`: cycle exists. If fast reaches null: no cycle.

---

### 33. Reverse Linked List in k-Groups
**TC:** O(N) | **SC:** O(N/k)

1. Count k nodes ahead. If fewer, return head as-is.
2. Reverse k nodes, tracking new head and tail.
3. Tail.next = reverseKGroup(nextGroup, k). Return new head.

---

### 34. Palindrome Linked List
**TC:** O(N) | **SC:** O(1)

1. Find middle with slow/fast pointers.
2. Reverse second half.
3. Compare first and reversed second half node by node.
4. Return whether all matched.

---

### 35. Start of Cycle in Linked List
**TC:** O(N) | **SC:** O(1)

1. Detect meeting point with Floyd's (slow/fast). If no cycle, return null.
2. Reset `slow = head`. Keep `fast` at meeting point.
3. Move both 1 step until they meet. Return meeting point = cycle start.

---

### 36. Flatten Linked List (sorted, with child pointers)
**TC:** O(N log N) | **SC:** O(1)

1. Recursively flatten from last list upward.
2. At each step, merge current list with already-flattened next list (merge two sorted lists using `bottom` pointer).

---

## DAY 7

### 37. Rotate Linked List by k
**TC:** O(N) | **SC:** O(1)

1. Find length N and tail. Connect tail to head (circular).
2. `k = k % N`. New tail is at position `N-k` from original head.
3. Advance `N-k-1` steps. New head = `newTail.next`. Break link.

---

### 38. Copy List with Random Pointer
**TC:** O(N) | **SC:** O(1)

1. Insert copy of each node right after: `1 -> 1' -> 2 -> 2'`.
2. Set random of copies: `node.next.random = node.random ? node.random.next : null`.
3. Separate original and copy lists.

---

### 39. 3 Sum
**TC:** O(N^2) | **SC:** O(1)

1. Sort array.
2. For each i (skip duplicates): `left=i+1`, `right=N-1`.
3. If sum==0: record, skip duplicates, left++, right--. If sum<0: left++. If sum>0: right--.

---

### 40. Trapping Rain Water
**TC:** O(N) | **SC:** O(1)

1. `left=0`, `right=N-1`, `leftMax=0`, `rightMax=0`, `water=0`.
2. While `left < right`: if `height[left] <= height[right]`: `water += max(0, leftMax - height[left])`, update leftMax, left++. Else: `water += max(0, rightMax - height[right])`, update rightMax, right--.

---

### 41. Remove Duplicates from Sorted Array
**TC:** O(N) | **SC:** O(1)

1. `slow=0`. For `fast` from 1: if `nums[fast] != nums[slow]`, slow++, `nums[slow] = nums[fast]`.
2. Return `slow+1`.

---

### 42. Max Consecutive Ones
**TC:** O(N) | **SC:** O(1)

1. `count=0`, `maxCount=0`. For each element: if 1, count++; else count=0. Update maxCount.

---

# GREEDY

### 43. N Meetings in One Room
**TC:** O(N log N) | **SC:** O(N)

1. Create (end, start) pairs. Sort by end time.
2. First meeting always selected. For each next: select if `start > last_selected_end`. Update lastEnd. Count selected.

---

### 44. Minimum Platforms Required
**TC:** O(N log N) | **SC:** O(1)

1. Sort arrival and departure arrays separately.
2. `i=0`, `j=0`, `platforms=0`, `maxPlatforms=0`.
3. While `i < N`: if `arrival[i] <= departure[j]`, platforms++, i++; else platforms--, j++. Update maxPlatforms.

---

### 45. Job Sequencing Problem
**TC:** O(N log N + N*D) | **SC:** O(D)

1. Sort jobs by profit descending.
2. `slots[maxDeadline]` boolean array.
3. For each job: find latest free slot <= deadline. If found, assign, add profit.

---

### 46. Fractional Knapsack
**TC:** O(N log N) | **SC:** O(1)

1. Calculate value/weight ratio for each item. Sort descending by ratio.
2. For each item: if full item fits, take it. Else take `(remaining capacity / weight) * value` fraction.

---

### 47. Minimum Number of Coins
**TC:** O(N * amount) | **SC:** O(amount)

**DP (general):** `dp[0]=0`. For each amount i, try all coins: `dp[i] = min(dp[i], dp[i-coin]+1)`.
**Greedy (standard denominations):** Sort desc, use as many of largest coin as possible, subtract.

---

### 48. Activity Selection
**TC:** O(N log N) | **SC:** O(1)

1. Sort activities by end time.
2. Select first. `lastEnd = activities[0].end`, `count=1`.
3. For each next: if `start >= lastEnd`, select, update lastEnd, count++.

---

# RECURSION & BACKTRACKING

### 49. Subset Sums
**TC:** O(2^N log 2^N) | **SC:** O(2^N)

1. Pick or don't pick each element. At base (index==N), add currentSum to result.
2. Sort result. Return it.

---

### 50. Subsets II (unique subsets with duplicates)
**TC:** O(2^N) | **SC:** O(2^N)

1. Sort array.
2. Backtrack: at each level, for index from start: skip if `i > start && arr[i] == arr[i-1]`.
3. Add current subset, recurse with index+1.

---

### 51. Combination Sum I (reuse allowed)
**TC:** O(2^T) | **SC:** O(T/min)

1. Sort candidates.
2. Backtrack: for each candidate from current index: add to path, recurse with **same index** (allow reuse), backtrack.
3. Base: if remaining==0, record. If remaining<0, return.

---

### 52. Combination Sum II (no reuse, no duplicate combos)
**TC:** O(2^N) | **SC:** O(N)

1. Sort candidates.
2. For each index from start: skip if `i > start && candidates[i] == candidates[i-1]`. Add, recurse with `i+1`, backtrack.

---

### 53. Palindrome Partitioning
**TC:** O(N * 2^N) | **SC:** O(N^2)

1. Precompute `isPalin[i][j]` DP table.
2. Backtrack: try all substrings from start. If `isPalin[start][end]`, add to path, recurse from end+1, backtrack.
3. Base: if start==N, record path.

---

### 54. Kth Permutation Sequence
**TC:** O(N^2) | **SC:** O(N)

1. Digit list = [1..N]. `k--` (0-indexed).
2. For each position: `index = k / (N-1)!`. Append `digits[index]`, remove it. `k %= (N-1)!`. Reduce factorial.

---

### 55. Rat in a Maze
**TC:** O(4^(N^2)) | **SC:** O(N^2)

1. From (0,0), try all 4 directions.
2. Move if in bounds, not visited, cell==1. Mark visited, recurse, unmark.
3. Base: if (N-1,N-1) reached, add path to result.

---

### 56. Word Search in Grid
**TC:** O(M*N * 4^L) | **SC:** O(L)

1. For each cell matching word[0], start DFS.
2. If index==word.length, return true. Check bounds, visited, char match.
3. Mark visited (`'#'`), recurse 4 directions, restore on backtrack.

---

### 57. N-Queens
**TC:** O(N!) | **SC:** O(N^2)

1. Backtrack row by row. Try each column.
2. Check: column set, diagonal1 set (row-col), diagonal2 set (row+col) — O(1) checks.
3. Place, recurse, remove. Base: row==N, record board.

---

### 58. Sudoku Solver
**TC:** O(9^81) | **SC:** O(1)

1. Find next empty cell.
2. Try digits 1-9: check valid (row, col, 3x3 box). Place, recurse. If returns true, done. Else backtrack.
3. No empty cell = solved, return true.

---

### 59. M-Coloring Problem
**TC:** O(M^N) | **SC:** O(N)

1. Try each color 1..M for each vertex. Check no adjacent vertex has same color.
2. If safe, assign, recurse. Unassign on backtrack.
3. Base: vertex==N, return true.

---

### 60. All Permutations
**TC:** O(N * N!) | **SC:** O(N)

**Swap-based:**
1. For current index to N-1: swap with current, recurse(current+1), swap back.
2. Base: current==N, add copy to result.

---

# BINARY SEARCH

### 61. Nth Root of a Number
**TC:** O(log(M) * N) | **SC:** O(1)

1. Binary search answer in [1, M]. For mid, compute `mid^N` (handle overflow).
2. If `mid^N == M`, return mid. If `< M`, left=mid+1. If `> M`, right=mid-1.

---

### 62. Median of Row-wise Sorted Matrix
**TC:** O(32 * M * log N) | **SC:** O(1)

1. Binary search on value range [min_element, max_element].
2. For each mid: count elements <= mid across all rows using binary search.
3. If count >= (M*N+1)/2: right=mid. Else left=mid+1. Return left.

---

### 63. Single Element in Sorted Array
**TC:** O(log N) | **SC:** O(1)

1. Binary search. If mid is odd, mid-- (ensure even index).
2. If `nums[mid] == nums[mid+1]`: single is on right, left=mid+2. Else right=mid.
3. Return `nums[left]`.

---

### 64. Search in Rotated Sorted Array
**TC:** O(log N) | **SC:** O(1)

1. Binary search. If `nums[left] <= nums[mid]`, left half is sorted.
2. If target in `[nums[left], nums[mid]]`, go left. Else go right.
3. Else right half sorted: if target in `[nums[mid], nums[right]]`, go right. Else go left.

---

### 65. Median of Two Sorted Arrays
**TC:** O(log(min(M,N))) | **SC:** O(1)

1. Binary search on shorter array. Partition: `cut1` on arr1, `cut2 = half - cut1` on arr2.
2. `l1=arr1[cut1-1]`, `r1=arr1[cut1]`, `l2=arr2[cut2-1]`, `r2=arr2[cut2]`.
3. If `l1<=r2 && l2<=r1`: valid partition. Median = `max(l1,l2)` (odd) or `(max(l1,l2)+min(r1,r2))/2` (even).
4. If `l1>r2`: move cut1 left. Else move right.

---

### 66. Kth Element of Two Sorted Arrays
**TC:** O(log(min(M,N))) | **SC:** O(1)

1. Binary search on smaller array. `cut1+cut2=k`. Verify `l1<=r2 && l2<=r1`.
2. If valid, return `max(l1,l2)`. Else adjust cuts.

---

### 67. Allocate Minimum Pages (Book Allocation)
**TC:** O(N * log(sum)) | **SC:** O(1)

1. Binary search on answer [max(pages), sum(pages)].
2. For each mid: greedily count students — accumulate pages, new student when adding next book exceeds mid.
3. If students needed <= M: right=mid. Else left=mid+1. Return left.

---

### 68. Aggressive Cows
**TC:** O(N log N + N * log(maxDist)) | **SC:** O(1)

1. Sort stall positions. Binary search on minimum distance.
2. For each mid: greedily place cows — first at stalls[0], next at first stall with distance >= mid.
3. If all cows placed: left=mid+1. Else right=mid-1. Return right.

---

# STACK & QUEUE

### 69. Implement Stack using Queues
**TC:** O(N) push, O(1) pop | **SC:** O(N)

1. Two queues Q1, Q2. Push: enqueue to Q2, move all Q1 to Q2, swap Q1 and Q2.
2. Pop/Top/Empty operate on Q1 directly.

---

### 70. Implement Queue using Stacks
**TC:** O(1) amortized | **SC:** O(N)

1. `inbox` (push), `outbox` (pop/peek).
2. Enqueue: push to inbox. Dequeue: if outbox empty, move all inbox to outbox. Pop from outbox.

---

### 71. Balanced Parentheses
**TC:** O(N) | **SC:** O(N)

1. For each char: opening → push. Closing → if stack empty or top doesn't match, return false. Else pop.
2. Return `stack.isEmpty()`.

---

### 72. Next Greater Element
**TC:** O(N) | **SC:** O(N)

1. Monotonic decreasing stack (stores elements).
2. For each element: pop while `stack.top <= current`. NGE = top if non-empty, else -1. Push current.
3. Circular: process 2N elements with `index % N`.

---

### 73. Sort a Stack
**TC:** O(N^2) | **SC:** O(N)

1. Recursively pop all. `sortedInsert(stack, element)`: if stack empty or top <= element, push. Else pop top, insert element, push top back.

---

### 74. LRU Cache
**TC:** O(1) all ops | **SC:** O(capacity)

1. HashMap (key → DLL node) + Doubly Linked List (head=most recent, tail=least recent).
2. Get: if exists, move node to head, return value. Else -1.
3. Put: if exists, update + move to head. Else create at head. If over capacity, remove tail from DLL and map.

---

### 75. Largest Rectangle in Histogram
**TC:** O(N) | **SC:** O(N)

1. Stack of indices (monotonic increasing heights).
2. For each bar: while stack non-empty and `heights[top] >= heights[i]`: pop top. Width = `i` if stack empty, else `i - stack.top - 1`. Area = `heights[top] * width`. Update max.
3. Push i. After all bars, continue popping with `i=N`.

---

### 76. Sliding Window Maximum
**TC:** O(N) | **SC:** O(K)

1. Deque (monotonic decreasing, stores indices).
2. For each i: remove front if out of window. Remove back while `nums[back] <= nums[i]`. Push i.
3. If `i >= k-1`, add `nums[deque.front()]` to result.

---

### 77. Min Stack
**TC:** O(1) all | **SC:** O(N)

1. Stack stores `(value, currentMin)` pairs.
2. Push: `currentMin = min(val, stack.top.min)`. Store pair.
3. GetMin: return `stack.top.min`.

---

### 78. Rotten Oranges
**TC:** O(M*N) | **SC:** O(M*N)

1. Add all rotten oranges to queue. Count fresh oranges.
2. BFS level by level (1 level = 1 minute): rot adjacent fresh, decrement fresh count.
3. If fresh==0, return minutes. Else return -1.

---

### 79. Stock Span Problem
**TC:** O(N) | **SC:** O(N)

1. Stack of (price, span) pairs.
2. For each price: span=1. While stack non-empty and `top.price <= current.price`: span += top.span, pop.
3. Push (price, span). Span = answer for this day.

---

### 80. Celebrity Problem
**TC:** O(N) | **SC:** O(1)

1. candidate=0. For i from 1 to N-1: if `candidate knows i`, candidate=i.
2. Verify: candidate knows nobody AND everybody knows candidate.
3. Return candidate or -1.

---

# STRINGS

### 81. Reverse Words in a String
**TC:** O(N) | **SC:** O(N)

1. Split by spaces. Reverse the array. Join with single space.
- **In-place:** Reverse entire string. Reverse each word individually.

---

### 82. Longest Palindromic Substring
**TC:** O(N^2) | **SC:** O(1)

1. For each center (2N-1 centers for odd+even): expand while `s[left] == s[right]`, left--, right++.
2. Track maximum length substring. Return it.

---

### 83. Roman to Integer
**TC:** O(N) | **SC:** O(1)

1. Map each symbol to value. Process right to left.
2. If `current value < previous value`: subtract. Else add.

---

### 84. Implement ATOI
**TC:** O(N) | **SC:** O(1)

1. Skip whitespace. Check sign. Parse digits.
2. At each step check overflow: if `result > (INT_MAX - digit) / 10`, return INT_MAX or INT_MIN.
3. `result = result * 10 + digit`. Apply sign.

---

### 85. Count and Say
**TC:** O(N * 2^N) | **SC:** O(2^N)

1. Start with "1". For each iteration: scan current, count consecutive same digits, append `count + digit`.
2. Return Nth string.

---

### 86. Compare Version Numbers
**TC:** O(max(M,N)) | **SC:** O(1)

1. Two pointers on both strings. Parse integer segment split by '.'.
2. Compare segments: if v1>v2 return 1, if v1<v2 return -1, else continue. Missing segments = 0.

---

### 87. Minimum Characters to Make Palindrome
**TC:** O(N) | **SC:** O(N)

1. Compute KMP failure function (LPS array) on `s + '#' + reverse(s)`.
2. Answer = `N - last_value_of_LPS_array`. These are chars to prepend.

---

### 88. Check if String is Rotation of Another
**TC:** O(N) | **SC:** O(N)

1. If lengths differ, return false.
2. Check if `s2` is substring of `s1 + s1` (using KMP or contains).

---

### 89. KMP Algorithm
**TC:** O(N+M) | **SC:** O(M)

**Build LPS array:**
1. `lps[0]=0`, `len=0`, `i=1`. While `i < M`: if `pattern[i]==pattern[len]`, `lps[i]=len+1`, i++, len++. Else if len>0, `len=lps[len-1]`. Else `lps[i]=0`, i++.

**Match:**
1. `i=0` (text), `j=0` (pattern). While `i < N`: if match, i++, j++. If j==M: found (report i-j), `j=lps[j-1]`. If mismatch and j>0: `j=lps[j-1]`. Else i++.

---

### 90. Rabin-Karp Algorithm
**TC:** O(N+M) avg | **SC:** O(1)

1. Compute hash of pattern and first window of text.
2. Slide window: `hash = (hash*base - leftChar*base^M + rightChar) % prime`.
3. If hashes match, verify by direct comparison (handle collisions).

---

# BINARY TREE

### 91. Inorder Traversal (Left → Root → Right)
**TC:** O(N) | **SC:** O(H)

**Iterative:** Push nodes going left. Pop, process. Move to right child, repeat.

---

### 92. Preorder Traversal (Root → Left → Right)
**TC:** O(N) | **SC:** O(H)

**Iterative:** Push root. Pop, process. Push right then left child.

---

### 93. Postorder Traversal (Left → Right → Root)
**TC:** O(N) | **SC:** O(H)

**Two stacks:** Modified preorder (root, right, left) → reverse = postorder.

---

### 94. Morris Inorder Traversal
**TC:** O(N) | **SC:** O(1)

1. `curr=root`. While curr not null:
   - No left child: process curr, move right.
   - Has left: find inorder predecessor (rightmost of left subtree).
     - If predecessor.right==null: thread it to curr, move left.
     - If predecessor.right==curr: remove thread, process curr, move right.

---

### 95. Level Order Traversal
**TC:** O(N) | **SC:** O(N)

1. Queue with root. While non-empty: record level size, dequeue all level nodes, process, enqueue children.

---

### 96. Zigzag Level Order
**TC:** O(N) | **SC:** O(N)

1. Level order. Alternate: add level normally or reversed using `leftToRight` flag (flip each level).

---

### 97. Vertical Order Traversal
**TC:** O(N log N) | **SC:** O(N)

1. BFS assigning (col, row) to each node. Root=(0,0). Left: col-1, Right: col+1.
2. Group by col. Within same col+row, sort by value. Output min to max col.

---

### 98. Boundary Traversal
**TC:** O(N) | **SC:** O(H)

1. Add root. Left boundary (top-down, exclude leaf). All leaves (left-right). Right boundary (bottom-up, exclude leaf).

---

### 99. Left View
**TC:** O(N) | **SC:** O(H)

**DFS:** Pass level. If `level == result.size()`, add node to result. Visit left before right.

---

### 100. Right View
**TC:** O(N) | **SC:** O(H)

**DFS:** If `level == result.size()`, add node. Visit right child before left.

---

### 101. Top View
**TC:** O(N log N) | **SC:** O(N)

1. BFS with (node, col). Ordered map `col → first seen node`. Enqueue left with col-1, right with col+1.

---

### 102. Bottom View
**TC:** O(N log N) | **SC:** O(N)

Same as top view but overwrite map (keep last seen = bottommost).

---

### 103. Height of Binary Tree
**TC:** O(N) | **SC:** O(H)

`height(node) = 0 if null, else 1 + max(height(left), height(right))`

---

### 104. Diameter of Binary Tree
**TC:** O(N) | **SC:** O(H)

1. DFS returns height but updates `maxDiam = max(maxDiam, leftHeight + rightHeight)` at each node.
2. Return `1 + max(left, right)`.

---

### 105. Check if Balanced
**TC:** O(N) | **SC:** O(H)

1. DFS returns height or -1 if unbalanced.
2. If left==-1 OR right==-1 OR `|left-right| > 1`: return -1. Else return `1 + max(left,right)`.

---

### 106. LCA of Binary Tree
**TC:** O(N) | **SC:** O(H)

1. Base: if null, p, or q → return node.
2. Recurse left and right. If both return non-null, current is LCA.
3. Return whichever side is non-null.

---

### 107. Maximum Path Sum
**TC:** O(N) | **SC:** O(H)

1. DFS: `leftGain = max(0, dfs(left))`, `rightGain = max(0, dfs(right))`.
2. Update `maxSum = max(maxSum, node.val + leftGain + rightGain)`.
3. Return `node.val + max(leftGain, rightGain)`.

---

### 108. Identical Trees
**TC:** O(N) | **SC:** O(H)

1. If both null → true. If one null or values differ → false.
2. Return `identical(left1,left2) && identical(right1,right2)`.

---

### 109. Symmetrical Tree
**TC:** O(N) | **SC:** O(H)

1. `isMirror(left, right)`: both null→true; one null or values differ→false.
2. Return `isMirror(left.left, right.right) && isMirror(left.right, right.left)`.

---

### 110. Flatten Binary Tree to Linked List
**TC:** O(N) | **SC:** O(1)

1. For each node with left child: find rightmost node of left subtree.
2. Connect that node's right to current's right. Move left to right. Set left=null. Advance to right.

---

### 111. Build Tree from Inorder + Preorder
**TC:** O(N) | **SC:** O(N)

1. First preorder element = root. Find in inorder (HashMap O(1)).
2. Left subtree = elements left of root in inorder. Recurse with corresponding preorder slice.

---

### 112. Build Tree from Inorder + Postorder
**TC:** O(N) | **SC:** O(N)

1. Last postorder element = root. Find in inorder. Split into left/right subtrees. Recurse (process right before left from postorder end).

---

### 113. Serialize and Deserialize Binary Tree
**TC:** O(N) | **SC:** O(N)

**Serialize:** BFS, append value or "null", separate by comma.
**Deserialize:** Split by comma. Queue-based BFS reconstruction. Next two values = left/right children.

---

### 114. Count Nodes in Complete Binary Tree
**TC:** O(log^2 N) | **SC:** O(log N)

1. `leftH` = go all left. `rightH` = go all right.
2. If equal: perfect tree → return `2^leftH - 1`. Else return `1 + count(left) + count(right)`.

---

### 115. Burn Tree from a Leaf
**TC:** O(N) | **SC:** O(N)

1. Map each node to its parent (BFS).
2. BFS from target node (treat as undirected using parent map).
3. Count BFS levels until queue empty. Answer = levels - 1.

---

### 116. Children Sum Property
**TC:** O(N) | **SC:** O(H)

1. If node.val < left + right: set node.val = left + right. Else set children's values = node.val (propagate downward).
2. After children recurse: update node = actual sum of children.

---

# BST

### 117. Search in BST
**TC:** O(H) | **SC:** O(1)

If null or val==target, return. If target < root.val, go left. Else go right.

---

### 118. Floor in BST (largest ≤ key)
**TC:** O(H) | **SC:** O(1)

1. `floor=-1`. Traverse: if val==key, return. If val>key, go left. If val<key, `floor=val`, go right.

---

### 119. Ceil in BST (smallest ≥ key)
**TC:** O(H) | **SC:** O(1)

1. `ceil=-1`. Traverse: if val==key, return. If val<key, go right. If val>key, `ceil=val`, go left.

---

### 120. Insert into BST
**TC:** O(H) | **SC:** O(H)

1. If null, create new node. If `val < root.val`, `root.left = insert(left, val)`. Else `root.right = insert(right, val)`. Return root.

---

### 121. Delete from BST
**TC:** O(H) | **SC:** O(H)

1. If no left child: return right. If no right child: return left.
2. Both children: find inorder successor (leftmost of right subtree). Replace node.val with successor.val. Delete successor from right.

---

### 122. Kth Smallest in BST
**TC:** O(H+K) | **SC:** O(H)

Iterative inorder: push left nodes. Pop, decrement k. If k==0, return value. Move to right, repeat.

---

### 123. Kth Largest in BST
**TC:** O(H+K) | **SC:** O(H)

Reverse inorder (right→root→left). Count until Kth element.

---

### 124. Validate BST
**TC:** O(N) | **SC:** O(H)

1. `validate(node, min, max)`. Initially `(-∞, +∞)`.
2. If `val <= min || val >= max`: false. Return `validate(left, min, val) && validate(right, val, max)`.

---

### 125. LCA in BST
**TC:** O(H) | **SC:** O(1)

1. If both p,q < root.val: go left. If both > root.val: go right. Else current root is LCA.

---

### 126. Construct BST from Preorder
**TC:** O(N) | **SC:** O(H)

1. `build(preorder, index, upperBound)`. If index>=N or preorder[index]>=bound: return null.
2. Root = preorder[index++]. Left = build with bound=root.val. Right = build with original bound.

---

### 127. BST Iterator
**TC:** O(1) amortized | **SC:** O(H)

1. Stack. Initialize: push all left nodes from root.
2. `next()`: pop, push all left nodes of popped.right. Return popped value.
3. `hasNext()`: stack non-empty.

---

### 128. Two Sum in BST
**TC:** O(N) | **SC:** O(N)

1. Forward BST iterator (smallest first) + Reverse BST iterator (largest first).
2. Two pointers: if sum==target, found. If < target, advance forward. If > target, advance reverse.

---

### 129. Recover BST (Two Swapped Nodes)
**TC:** O(N) | **SC:** O(H)

1. Inorder traversal. Track `prev`, `first`, `middle`, `last`.
2. First violation (`prev.val > curr.val`): `first=prev`, `middle=curr`.
3. Second violation: `last=curr`.
4. Swap `first` with `last` (two violations) or `first` with `middle` (one violation).

---

### 130. Largest BST in Binary Tree
**TC:** O(N) | **SC:** O(H)

1. DFS returns `(isBST, size, min, max)` per subtree.
2. Valid if both subtrees valid BSTs AND `left.max < node.val < right.min`. Size = left.size + right.size + 1. Update global max.

---

# GRAPH

### 131. Clone Graph
**TC:** O(V+E) | **SC:** O(V)

1. BFS/DFS. HashMap: original → clone.
2. For each node: create clone. For each neighbor: create clone if not exists, add to current clone's neighbors.

---

### 132. DFS Traversal
**TC:** O(V+E) | **SC:** O(V)

Mark visited, process, recursively visit all unvisited neighbors. Use visited array.

---

### 133. BFS Traversal
**TC:** O(V+E) | **SC:** O(V)

Queue with source. Mark visited. While non-empty: dequeue, process, enqueue unvisited neighbors.

---

### 134. Detect Cycle — Undirected Graph
**TC:** O(V+E) | **SC:** O(V)

**BFS:** Queue with (node, parent). If neighbor is visited and not parent → cycle.
**DFS:** If visited neighbor != parent → cycle.

---

### 135. Detect Cycle — Directed Graph
**TC:** O(V+E) | **SC:** O(V)

**DFS with colors (WHITE=0, GRAY=1, BLACK=2):**
1. Mark GRAY on entry. If neighbor is GRAY → cycle (back edge). Mark BLACK on exit.

---

### 136. Topological Sort (DFS)
**TC:** O(V+E) | **SC:** O(V)

1. DFS from each unvisited node. After all neighbors processed, push to stack.
2. Pop stack = topological order.

---

### 137. Topological Sort — Kahn's Algorithm (BFS)
**TC:** O(V+E) | **SC:** O(V)

1. Compute in-degrees. Queue all nodes with in-degree 0.
2. Dequeue, add to result, decrement neighbors' in-degrees. Enqueue if in-degree becomes 0.
3. If result.size != V → cycle exists.

---

### 138. Number of Islands
**TC:** O(M*N) | **SC:** O(M*N)

For each unvisited '1': DFS/BFS marking all connected land as visited. Increment count per initiation.

---

### 139. Bipartite Check
**TC:** O(V+E) | **SC:** O(V)

BFS coloring. Assign color 0 to source. Neighbors get opposite color. If neighbor same color → not bipartite. Check all components.

---

### 140. Kosaraju's SCC
**TC:** O(V+E) | **SC:** O(V)

1. DFS on original graph. Push to stack by finish time.
2. Transpose graph (reverse all edges).
3. DFS on transposed graph popping stack. Each DFS call = one SCC.

---

### 141. Dijkstra's Algorithm
**TC:** O((V+E) log V) | **SC:** O(V)

1. Min-heap with (dist, node). All dist=∞, source=0.
2. Pop min. For each neighbor: if `dist[node] + weight < dist[neighbor]`, update and push.

---

### 142. Bellman-Ford
**TC:** O(V*E) | **SC:** O(V)

1. All dist=∞, source=0. Relax all edges V-1 times.
2. If any edge relaxable on Vth pass → negative cycle.

---

### 143. Floyd-Warshall
**TC:** O(V^3) | **SC:** O(V^2)

`dist[i][j] = edge weight or ∞`. For each k: for each (i,j): `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`.

---

### 144. Prim's MST
**TC:** O(E log V) | **SC:** O(V)

1. Min-heap with (weight, node). Start (0, source).
2. Pop min. If in MST, skip. Else add to MST, add weight. Push all adjacent unvisited edges.

---

### 145. Kruskal's MST
**TC:** O(E log E) | **SC:** O(V)

1. Sort edges by weight. Initialize DSU.
2. For each edge: if `find(u) != find(v)`, add to MST, `union(u,v)`. Stop at V-1 edges.

---

### 146. Number of Provinces
**TC:** O(V^2) | **SC:** O(V)

DFS/BFS on adjacency matrix. For each unvisited city, DFS to mark all connected. Increment count.

---

### 147. Alien Dictionary
**TC:** O(N*L + V+E) | **SC:** O(V+E)

1. Compare adjacent words to get character ordering edges. Invalid if word2 is prefix of word1.
2. Topological sort on characters. Cycle → return "". Return topo order.

---

### 148. Word Ladder
**TC:** O(N * L^2) | **SC:** O(N*L)

1. BFS from beginWord. All words in set.
2. Change each character to 'a'-'z'. If new word in set: enqueue, remove from set, level++.
3. If endWord reached, return level. Return 0 if not found.

---

# DYNAMIC PROGRAMMING

### 149. Maximum Product Subarray
**TC:** O(N) | **SC:** O(1)

1. Track `maxProd`, `minProd`, `result`. For each element: `tempMax = max(num, num*maxProd, num*minProd)`. Update minProd similarly. Update result.

---

### 150. Longest Increasing Subsequence (LIS)
**TC:** O(N log N) | **SC:** O(N)

**Patience Sorting:**
1. `tails[]` array. For each element: binary search for leftmost tail >= element (lower_bound). Replace, or append if element is largest.
2. `tails.length` = LIS length.

**O(N^2) DP:** `dp[i] = LIS ending at i = max(dp[j]+1) for j<i where nums[j]<nums[i]`.

---

### 151. Longest Common Subsequence (LCS)
**TC:** O(M*N) | **SC:** O(M*N)

1. `dp[i][j]` = LCS of s1[0..i-1] and s2[0..j-1].
2. If `s1[i-1]==s2[j-1]`: `dp[i][j] = dp[i-1][j-1]+1`. Else `max(dp[i-1][j], dp[i][j-1])`.

---

### 152. 0/1 Knapsack
**TC:** O(N*W) | **SC:** O(W)

1. 1D dp, size W+1. For each item: iterate `w` from W down to weight[i]: `dp[w] = max(dp[w], dp[w-weight[i]] + value[i])`.

---

### 153. Edit Distance
**TC:** O(M*N) | **SC:** O(M*N)

1. `dp[i][j]` = min edits to convert word1[0..i-1] to word2[0..j-1]. Base: `dp[i][0]=i`, `dp[0][j]=j`.
2. If chars equal: `dp[i][j] = dp[i-1][j-1]`. Else `1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])` (delete, insert, replace).

---

### 154. Matrix Chain Multiplication
**TC:** O(N^3) | **SC:** O(N^2)

1. `dp[i][j]` = min cost to multiply matrices i to j.
2. For length l from 2: for each start i, j=i+l-1: for each split k: `dp[i][j] = min(dp[i][j], dp[i][k] + dp[k+1][j] + dims[i-1]*dims[k]*dims[j])`.

---

### 155. Minimum Path Sum in Grid
**TC:** O(M*N) | **SC:** O(M*N)

1. `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`. Base: first row/col = cumulative sums.

---

### 156. Coin Change (Minimum Coins)
**TC:** O(N*amount) | **SC:** O(amount)

1. `dp[0]=0`, all others=∞. For each amount i, each coin c: `dp[i] = min(dp[i], dp[i-c]+1)`.
2. Return `dp[amount]` if ≠∞, else -1.

---

### 157. Subset Sum
**TC:** O(N*sum) | **SC:** O(sum)

1. `dp[j]` = can we achieve sum j. `dp[0]=true`.
2. For each element, iterate j from sum down to arr[i]: `dp[j] = dp[j] || dp[j-arr[i]]`.

---

### 158. Rod Cutting
**TC:** O(N^2) | **SC:** O(N)

1. `dp[i]` = max revenue from rod of length i. For each length i, each cut j from 1 to i: `dp[i] = max(dp[i], price[j] + dp[i-j])`.

---

### 159. Egg Dropping Problem
**TC:** O(E * N log N) | **SC:** O(E*N)

**DP on trials:** `dp[e][f]` = max floors testable with e eggs, f trials. `dp[e][f] = dp[e-1][f-1] + dp[e][f-1] + 1`. Find min f where `dp[eggs][f] >= N`.

---

### 160. Word Break
**TC:** O(N^2) | **SC:** O(N)

1. `dp[i]` = can s[0..i-1] be segmented. `dp[0]=true`.
2. For each i: for each j<i: if `dp[j]` and `s[j..i-1]` in dict: `dp[i]=true`.

---

### 161. Partition Equal Subset Sum
**TC:** O(N*sum) | **SC:** O(sum)

1. If total sum is odd → false. Target = sum/2.
2. Subset sum DP: `dp[j] = dp[j] || dp[j-nums[i]]` (iterate j from target down to nums[i]).

---

### 162. LIS using Binary Search
Same as Problem 150 — Patience Sorting approach. **TC: O(N log N)**.

---

# HEAPS

### 163. Kth Largest Element
**TC:** O(N log K) | **SC:** O(K)

Min-heap size K. For each element: push, pop if size > K. Top = Kth largest.

---

### 164. Maximum Sum Combination
**TC:** O(K log K) | **SC:** O(K)

1. Sort both arrays descending. Max-heap with (sum, i, j), start (A[0]+B[0], 0, 0).
2. Pop K times. Push (A[i+1]+B[j], i+1, j) and (A[i]+B[j+1], i, j+1) if not visited (use set).

---

### 165. Find Median from Data Stream
**TC:** O(log N) add, O(1) find | **SC:** O(N)

1. `maxHeap` (left half, smaller numbers) + `minHeap` (right half, larger numbers).
2. Add: push to maxHeap. Move maxHeap.top to minHeap. If minHeap.size > maxHeap.size, move back.
3. Median: if equal sizes → `(maxHeap.top + minHeap.top) / 2.0`. Else `maxHeap.top`.

---

### 166. Merge K Sorted Arrays
**TC:** O(N log K) | **SC:** O(K)

1. Min-heap with (value, arrayIdx, elemIdx). Init with first element of each array.
2. Pop min → add to result. Push next element from same array.

---

### 167. K Most Frequent Elements
**TC:** O(N log K) | **SC:** O(N)

1. Count frequencies (HashMap). Min-heap of size K on (frequency, element).
2. For each entry: push. If size > K, pop. Return all in heap.

---

### 168. Task Scheduler
**TC:** O(N) | **SC:** O(1)

1. Count frequencies. `maxFreq = highest frequency`. `countMaxFreq = number of tasks with maxFreq`.
2. `result = max(N, (maxFreq-1)*(n+1) + countMaxFreq)`.

---

# TRIE

### 169. Implement Trie I (Insert, Search, StartsWith)
**TC:** O(L) per op | **SC:** O(N*L)

- **Node:** `children[26]`, `isEnd`.
- **Insert:** For each char, create child if not exists, traverse. Mark last as end.
- **Search:** Traverse. If any char missing → false. Return `isEnd` at last node.
- **StartsWith:** Traverse. If any char missing → false. Return true (don't check isEnd).

---

### 170. Implement Trie II (with prefix/word counts)
**TC:** O(L) per op | **SC:** O(N*L)

- **Node:** `children[26]`, `wordCount`, `prefixCount`.
- **Insert:** Increment `prefixCount` at each node, `wordCount` at terminal.
- **CountWordsEqualTo:** Traverse, return `wordCount`.
- **CountWordsStartingWith:** Traverse, return `prefixCount`.
- **Erase:** Decrement both counts on path.

---

### 171. Longest String with All Prefixes
**TC:** O(N*L) | **SC:** O(N*L)

1. Insert all words into trie.
2. DFS: only continue if `isEnd=true` at each node (every prefix is a word).
3. Track longest valid string. Tie-break: lexicographically smaller.

---

### 172. Count Distinct Substrings
**TC:** O(N^2) | **SC:** O(N^2)

1. Insert all suffixes of string into trie.
2. Count total nodes created = number of distinct substrings.

---

### 173. Maximum XOR of Two Numbers
**TC:** O(N * 32) | **SC:** O(N * 32)

1. Insert all numbers into binary trie (MSB to LSB).
2. For each number: greedily traverse opposite bit path. If opposite exists, take it (XOR bit = 1). Else take same.
3. Return maximum XOR found.

---

### 174. Maximum XOR with Element from Array (Offline)
**TC:** O((N+Q) log maxVal) | **SC:** O(N*32)

1. Sort queries by m. Sort array.
2. For each query (x, m): insert all array elements ≤ m into trie. Find max XOR of x with trie.
3. If no element ≤ m: answer = -1.

---

### 175. Complete String
**TC:** O(N*L) | **SC:** O(N*L)

Insert all words. For each word: check if every prefix also exists as a word (every node on path has `isEnd=true`). Track longest such word.

---

# QUICK REFERENCE — KEY PATTERNS

```
Sliding Window    → Longest/shortest subarray, max in window
Two Pointers      → Sorted array, 3sum, palindrome, rain water
Prefix Sum/XOR    → Subarray count/sum problems
Monotonic Stack   → Next greater/smaller element, histogram
BFS               → Shortest path, multi-source, level order
DFS + Backtrack   → Permutations, combinations, maze, N-Queens
Binary Search     → "Find min/max satisfying a condition"
Union-Find (DSU)  → Connected components, Kruskal's MST
Floyd's Algorithm → Cycle detection, duplicate finding
Greedy + Sort     → Activity selection, job scheduling
```

---

**Backtracking Template:**
```java
void backtrack(state, choices) {
    if (baseCase) { record(); return; }
    for (choice : choices) {
        makeChoice();
        backtrack(newState, remainingChoices);
        undoChoice();
    }
}
```

**DP Template:**
```
1. Define state: what does dp[i] or dp[i][j] mean?
2. Base cases
3. Transition: dp[i] = f(dp[i-1], dp[i-2], ...)
4. Answer: where in dp table?
```

---

*Total: 175 problems | Focus for Amazon SDE2: Arrays, DP, Graphs, Trees, Stack/Queue*
