# Notes on LeetCode questions

## Graph

- Modeling state changes, relationships, or path traversals as graph problems is very useful
- Graph connectivity problems can be solved with union find sometimes
- It's okay to revisit a node in the graph if we need more than just a `boolean` flag to represent the "visited" state
- Approaching a graph problem by constructing DFS tree can be useful. It essentially remove all cross, forward, and backward edges and only leave tree edges
- Another use case of topological sort is when we need to traverse a tree/graph from its leaf nodes and move inward

## Binary search

- We use binary search to eliminate the half of the search space where the answer **cannot** be in
- Some unintuitive scenarios where binary search may be used:
    - Divide an array of non-negative integers into consecutive subarrays where the sum of each subarray need to satisfy some properties (e.g., `<=` some threshold). We either fix the number of consecutive subarrays and find the threshold, or we fix the threshold and find the number of consecutive subarrays. Binary search works here because all numbers are non-negative, so if one subarray is longer than another, then its sum must be `>=` the other as well
    - Find the `k`-th smallest element (where `k` could be `1` or `n`). Binary search can be useful here if we can identify the range of the element. If the element satisfies the property of binary search (e.g., element is numeric value), then we can count the number of elements that are `<=` than the search target. If we have a fast way to count the elements (e.g., `O(n)` where `n` is the total number of elements), then the total time complexity is `O(n * log(search_space))` where `search_space` is the range of element. Depending on the problem it can be faster than sorting or using a heap.
    - Find the longest consecutive subarray that satisfies some property. Binary search works here if we can prove that given a subarray of length `l` that satisfies the property, we can find a sub-subarray for every length `l' < l` inside that subarray that also satisfies the property

## Backtracking

Backtracking is essentially a DFS traversal over the recursion tree; each recursive call is like visiting a node in the recursion tree. Often we need to provide a way to let recursive call to choose what child nodes to visit (e.g., an index or a value)

## Avoiding duplicate sequences in O(1)

- If order matters, then we need to avoid sequences that start/end with the same prefix/suffix
- If order doesn't matter, then one way is to limit the size of input we consider and gradually expand it in each iteration

## Dealing with pairs or ranges

- If we need to find a pair of elements that satisfies some property, it's worthwhile to approach the problem from the perspective of starting/ending point: if the current element is the starting/ending point of the optimal solutio, which element could be the corresponding ending/starting point? If we can find an `O(1)` way to decide that, then we can achieve `O(n)` instead of `O(n^2)` total time complexity. Note that sometimes it's possible to have multiple candidates. We can make use of some data structures (such as deque or binary search tree) to achieve `O(1)` or `O(logn)` to decide the best starting/ending point
- If we need to find a consecutive subrange that satisfies some property, instead of looping through every possible subrange (which is `O(n^2)`), we can try to find for each element, what is the left and right boundary that satiesfy the property. We may be able to do it in `O(n)` time (once for left boundary and once for right boundary)

## Intervals

- Sort intervals by starting/ending point depending on the problem
- Treat each endpoint as an "event" by sorting and processing the endpoints rather than the intervals themselves

## Sliding window

- Sliding window is useful to find subranges that satisfy some required constraints of element counts (applies to all below scenarios)
- Sliding window is useful when you need to "fill the window". E.g., you need to make a subrange with fixed length such that after swapping `x` number of elements, all elements inside the window are the same (or are consecutive). We can have a sliding window of fixed length, and compute how many elements inside this window need to be replaced
- If the problem involves ranges or pair of indicies, and it has a hard requirement on the upper bound of the length of the range or difference between the pair of indicies, then we can also treat it as a sliding window problem
- One trick is that if we only care about longest sliding window, then we may not need to shrink the window; we only need to shift it. Sometimes it can make computation easier

## Merge sort

If we find ourselves in need of maintaining a dynamic binary search tree where each node maintains the count of its subtree, then a modified merge sort algorithm may be helpful. The idea is that we use sorted left/right half to maintain the sorted property, and use the merge step to count whatever we need

## Heap

- If we need to find the `k`-th smallest element in an unsorted input, a max heap is useful here as we essentially store the k smallest elements in reverse order in the heap. Whenever the size of the heap is larger than `k` we pop one element off the heap. This gives `O(nlogk)` instead of `O(nlogn)` of a naive sort solution
- However, if the input is already sorted but it requires more computation to calculate the `k`-th smallest element from the input (in other words, we can't get the `k`-th smallest element in `O(1)` time), then a min heap might be useful here. We pop elements `k` times from the heap; the `k`-th element is the one we need. This takes `O(klogn)` where `n` is the total size of the input
- `k`-th largest element is just the mirror of the above problems

## Monotonic stack and deque

- Monotonic deque is useful if we need to maintain the max/min element in a sliding window of fixed size
- Monotonic stack is useful to solve the previous/next smaller/larger element problem; what this implies is that we need to process the input such that it has a sorted order while not changing the original relative positioning

## Misc

- If we can categorize an array of elements into two categories, then we can treat each category as `+1` and `-1` and see if it simplifies the problem
- Prefix sum (and suffix and total sum) is usually helpful when dealing with sums of consecutive subranges
- When dealing with 2D matricies, sometimes it's helpful to reduce the problem to 1d array on one dimension, and solve the 1d array problem. Usually this is helpful when traversing every matrix element (or every pair of upper left/lower right indicies) is too slow
- Similar to above, if a problem has multiple constraints, sometimes it's helpful to solve a problem with less constraints, and extend this solution of the simpler problem to solve the original, more complicated problem
- Given a tree problem, it's very useful to figure out the traversal order (in-order vs pre-order vs post-order)
- If the problem involves two kind of operations that are mirror of each other, it may be worthwhile to model both operations using a single approach (we may need to take care of directions)
- If the problem asks to find a single element that matches some criteria, we could approach the problem by eliminating one element that **does not** match the criteria and solve the smaller problem recursively. We may need to verify the final candidate that it indeed matches the criteria

# Related questions

- 4, 295, 480
- 10, 44, 72
- 31, 670, 1053
- 42, 11, 654, 1130
- 76, 438, 1358, 992
- 84, 85, 907
- 99, 334
- 105, 106, https://www.geeksforgeeks.org/construct-tree-inorder-level-order-traversals-set-2/
- 109, 99
- 142, 287
- 161, 680
- 222, 655, 779
- 224, 227 (282), 772 (1597)
- 239, 683, 1696
- 240, 302, 1428
- 249, 694, 205, 1072
- 282 (1597), 679, 241
- 296, 1478, 317, 1515
- 297, 428
- 310, 366
- 312, 936, 880
- 315, 327, 493
- 354, 1626
- 363, 1074, 750
- 378, 719, 373, 1439
- 394, 636, 726, 1096
- 395, 795
- 406, https://www.cnblogs.com/jingjingblog/p/9569822.html
- 410 (1335), 1011, 1231, 774
- 424, 1156
- 464, 913
- 480, 295, 4
- 546, 664
- 552, 1223, 920, 1411
- 581, 1375
- 630, 1353, 857, 502, 1383, 871
- 683, 1375
- 685, 1192
- 730, 940
- 741, 818
- 753, 332
- 757, 435
- 759, 1094
- 765, 1202
- 767, 984, 1405, 1054, 358, 621
- 778, 1482
- 801, 1007
- 834, 968, 979
- 843, 887, 375
- 862, 962
- 864, 1293
- 1024, 1326
- 1060, 1539
- 1144, 280, 324
- 1547, 1000