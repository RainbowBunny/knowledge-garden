---
{"dg-publish":true,"permalink":"/knowledge/cs/algorithms/sorting/","dg-note-properties":{}}
---


## Sorting Problem

> [!definition] Sorting Problem
> 
> **Input**: A sequence of $n$ numbers $\langle a_1, a_2, \dots, a_n \rangle$.
> **Output**: A permutation (reordering) $\langle a_1', a_2', \dots, a_n' \rangle$ of the input sequence such that $a_1' \leq a_2' \leq \cdots \leq a_n'$.

| Algorithm      | Worst-case running time | Average-case/expected running time |
| -------------- | ----------------------- | ---------------------------------- |
| Insertion sort | $\Theta(n^2)$           | $\Theta(n^2)$                      |
| Merge sort     | $\Theta(n \log n)$      | $\Theta(n \log n)$                 |
| Heapsort       | $O(n \log n)$           | -                                  |
| Quicksort      | $\Theta(n^2)$           | $\Theta(n \ln n)$ (expected)       |
| Counting sort  | $\Theta(k + n)$         | $\Theta(k + n)$                    |
| Radix sort     | $\Theta(d(n + k))$      | $\Theta(d(n + k))$                 |
| Bucket sort    | $\Theta(n^2)$           | $\Theta(n)$ (average-case)         |
> [!theorem]
> Any comparison sort algorithm requires $\ohm(n \log n)$ comparisons in the worst case.

> [!definition] Stable
> A sorting algorithm is **stable** if numbers with the same value appear in the output array in the same order as they do in the input array.

> [!definition] In Place
> An algorithm is **in place** if only a constant number of elements of the input array are ever sorted outside the array.

> [!definition] Inversions
> Let `A[1..n]` be an array of $n$ distinct numbers. If `i < j` and `A[i] > A[j]`, then the pair `(i, j)` is called an **inversion** of `A`.

### Insertion Sort

> [!pseudocode]
> ```
> INSERTION-SORT(A)
> 1. for j = 2 to A.length
> 2.     key = A[j]
> 3.	   // Insert A[j] into the sorted sequence A[1..j-1]
> 4.	   i = j - 1
> 5.	   while i > 0 and A[i] > key
> 6.		   A[i + 1] = A[i]
> 7.		   i = i - 1
> 8.	   A[i + 1] = key
> ```

### Selection Sort

> [!pseudocode]
> ```
> SELECTION-SORT(A)
> 1. for i = 1 to A.length - 1
> 2.     minIndex = i
> 3.     for j = i + 1 to A.length
> 4.         if A[j] < A[minIndex]
> 5.             minIndex = j
> 6.     exchange A[i] with A[minIndex]
> ```

### Merge Sort

> [!definition] Merge Sort algorithm
> **Divide**: Divide the $n$-element sequence to be sorted into two subsequences of $n/2$ elements each.
> **Conquer**: Sort the two subsequences recursively using merge sort.
> **Combine**: Merge the two sorted subsequences to produce the sorted answer.

> [!pseudocode]
> ```
> MERGE(A, p, q, r)
>  1. n1 = p - q + 1
>  2. n2 = r - q
>  3. Let L[1..n1 + 1] and R[1..n2 + 1] be new arrays
>  4. for i = 1 to n1
>  5.     L[i] = A[p + i - 1]
>  6. for j = 1 to n2
>  7.     R[j] = A[q + j]
>  8. L[n1 + 1] = INF
>  9. R[n2 + 1] = INF
> 10. i = 1
> 11. j = 1
> 12. for k = p to r
> 13.     if L[i] <= R[j]
> 14.         A[k] = L[i]
> 15.         i = i + 1
> 16.     else A[k] = R[j]
> 17.         j = j + 1
> ```

> [!pseudocode]
> ```
> MERGE-SORT(A, p, r)
> 1. if p < r
> 2.     q = FLOOR((p + r) / 2)
> 3.     MERGE-SORT(A, p, q)
> 4.     MERGE-SORT(A, q + 1, r)
> 5.     MERGE(A, p, q, r)
> ```

### Bubble Sort

> [!pseudocode]
> ```
> BUBBLE-SORT(A)
> 1. for i = 1 to A.length - 1
> 2.     for j = A.length downto i + 1
> 3.         if A[j] < A[j - 1]
> 4.             exchange A[j] with A[j - 1]
> ```

### Heapsort

> [!pseudocode]
> ```
> HEAPSORT(A)
> 1. BUILD-MAX-HEAP(A)
> 2. for i = A.length downto 2
> 3.     exchange A[1] with A[i]
> 4.     A.heap-size = A.heap-size - 1
> 5.     MAX-HEAPIFY(A, 1)
> ```

### Quicksort

> [!definition] Quicksort
> **Divide**: Partition (rearrange) the array $A[p..r]$ into two (possibly empty) subarrays $A[p..q - 1]$ and $A[q + 1..r]$ such that each element of $A[p..q - 1]$ is less than or equal to $A[q]$, which is, in turn, less than or equal to each element of $A[q + 1..r]$. Compute the index $q$ as part of this partitioning procedure.
> **Conquer**: Sort the two subarrays $A[p..q - 1]$ and $A[q + 1..r]$ by recursive calls to quicksort.
> **Combine**: Because the subarrays are already sorted, no work is needed to combine them: the entire array $A[p..r]$ is now sorted.

> [!pseudocode]
> ```
> PARTITION(A, p, r)
> 1. x = A[r]
> 2. i = p - 1
> 3. for j = p to r - 1
> 4.     if A[j] <= x
> 5.         i = i + 1
> 6.         exchange A[i] with A[j]
> 7. exchange A[i + 1] with A[r]
> 8. return i + 1
> 
> QUICKSORT(A, p, r)
> 1. if p < r
> 2.     q = PARTITION(A, q, r)
> 3.     QUICKSORT(A, p, q - 1)
> 4.     QUICKSORT(A, q + 1, r)
> ```

> [!pseudocode]
> ```
> RANDOMIZED-PARTITION(A, p, r)
> 1. i = RANDOM(p, r)
> 2. exchange A[r] with A[i]
> 3. return PARTITION(A, p, r)
> 
> RANDOMIZED-QUICKSORT(A, p, r)
> 1. if p < r
> 2.     q = RANDOMIZED-PARTITION(A, q, r)
> 3.     RANDOMIZED-QUICKSORT(A, p, q - 1)
> 4.     RANDOMIZED-QUICKSORT(A, q + 1, r)
> ```

> [!lemma]
> Let $X$ be the number of comparisons performed in line $4$ of the `PARTITION` over the entire execution of `QUICKSORT` on an $n$-element array. Then the running time of `QUICKSORT` is $O(n + X)$.

> [!remark]
> $E[X] = O(n \log n)$

**Hoare partition**.

> [!pseudocode]
> ```
> HOARE-PARTITION(A, p, r)
>  1. x = A[p]
>  2. i = p - 1
>  3. j = r + 1
>  4. while TRUE
>  5.     repeat
>  6.         j = j - 1
>  7.     until A[j] <= x
>  8.     repeat
>  9.         i = i + 1
> 10.     until A[i] >= x
> 11.     if i < j
> 12.         exchange A[i] with A[j]
> 13.     else return j
> ```

**Quicksort with equal element values**

> [!pseudocode]
> ```
> PARTITION(A, p, r)
>  1. x = A[r]
>  2. lt = p // boundary of < x
>  3. i = p // current element
>  4. gt = r // boundary of > x
>  5. while i <= gt
>  6.     if A[i] < x
>  7.         exchange A[lt] with A[i]
>  8.         lt = lt + 1
>  9.         i = i + 1
> 10.     else if A[i] > x
> 11.         exchange A[i] with A[gt]
> 12.         gt = gt - 1
> 13.     else
> 14.         i = i + 1
> 15. return (lt, gt)
> 
> QUICKSORT(A, p, r)
> 1. if p < r
> 2.     (lt, gt) = PARTITION(A, p, r)
> 3.     QUICKSORT(A, p, lt - 1)
> 4.     QUICKSORT(A, gt + 1, r)
> ```

**Tail Recursion**:

> [!pseudocode]
> ```
> TAIL-RECURSIVE-QUICKSORT(A, p, r)
> 1. while p < r
> 2.     q = PARTITION(A, p, r)
> 3.     if (q - p) < (r - q)
> 4.         TAIL-RECURSIVE-QUICKSORT(A, p, q - 1)
> 5.         p = q + 1
> 6.     else
> 7.         TAIL-RECURSIVE-QUICKSORT(A, q + 1, r)
> 8.         r = q - 1
> ```

### Counting Sort

> [!remark]
> **Counting sort** works for $n$ input elements is an integer in the range $0$ to $k$, for some integer $k$. Thus we should use this when $k = O(n)$.

> [!pseudocode]
> ```
> COUNTING-SORT(A, B, k)
>  1. let C[0..k] be a new array
>  2. for i = 0 to k
>  3.     C[i] = 0
>  4. for j = 1 to A.length
>  5.     C[A[j]] = C[A[j]] + 1
>  6. // C[i] now contains the number of elements equal to i.
>  7. for i = 1 to k
>  8.     C[i] = C[i] + C[i - 1]
>  9. // C[i] now contains the number of elements less than or equal to i.
> 10. for j = A.length downto 1
> 11.     B[C[A[j]]] = A[j]
> 12.     C[A[j]] = C[A[j]] - 1
> ```

### Radix Sort

> [!remark]
> **Radix sort** works for $d$-digit numbers ($d$ column).
> 

> [!pseudocode]
> ```
> RADIX-SORT(A, d)
> 1. for i = 1 to d
> 2.     use a stable sort to sort array A on digit i
> ```

> [!lemma]
> Given $n$ $d$-digit numbers in which each digit can take on up to $k$ possible values, `RADIX-SORT` correctly sorts these numbers in $\Theta(d(n + k))$ time if the stable sort it uses takes $\Theta(n + k)$ time.

> [!lemma]
> Given $n$ $b$-bit numbers and any positive integer $r \leq b$, `RADIX-SORT` correctly sorts these numbers in $\Theta((\frac{b}{r})(n + 2^r))$ time if the stable sort it uses takes $\Theta(n + k)$ time for inputs in the range $0$ to $k$.

### Bucket Sort

> [!remark]
> **Bucket sort** assumes that the input is drawn from a uniform distribution and has an average-case running time of $O(n)$. In this situation, assume that the input is generated by a random process that distributes elements uniformly and independently over the interval $[0, 1)$.

> [!pseudocode]
> ```
> BUCKET-SORT(A)
> 1. let B[0..n - 1] be a new array
> 2. n = A.length
> 3. for i = 0 to n - 1
> 4.     make B[i] an empty list
> 5. for i = 1 to n
> 6.     insert A[i] into list B[FLOOR(nA[i])]
> 7. for i = 0 to n - 1
> 8.     sort list B[i] with insertion sort
> 9. concatenate the lists B[0], B[1], ..., B[n - 1] together in order
> ```
