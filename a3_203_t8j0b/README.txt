
Put your answers to non-coding questions in this file as described in
the assignment description.

All answers are to be in plain text ASCII.

Part 2, cache miss rate

Question a. An array of long with 8 rows and 128 columns, a direct-mapped cache, and the function sumA from the program cache-test provided in the first part of the assignment.

Answer a. sumA accesses elements in a row-major order (outer loop iterates over the rows, inner loop iterates over the columns). The size of each block is 64 bytes, meaning it can store up to 8 long elements. In total we have 1024 elements (8 rows * 128 columns) that we need to access. The program will have to make 8 cache calls, since we have a room for 8 longs in each line, and since it's a direct-mapped cache it will miss 1/8 times, meaning our miss rate is 12.5%.

Question b. An array of long with 8 rows and 128 columns, a direct-mapped cache, and the function sumB from the program cache-test provided in the first part of the assignment.

Answer b. Since the parameters are the same as for Question a, we will need to assess the difference between sumA and sumB. sumB accesses data in the column-major order. Since the arrays are defined to be stored in row-major order that means that our cache will miss every time, since we are requesting data pertaining to a different row every time. So, the cache miss will 100%.

Question c. An array of long with 8 rows and 128 columns, a direct-mapped cache, and the function sumC from the program cache-test provided in the first part of the assignment.

Answer c. The loops are again set up for a column-major order, similar to sumB, however, we have a different way to call the cache_read method. The access pattern we get is a[i][j], a[i][j+1], a[i+1][j], a[i+1][j+1], which lead us to a miss-hit-miss-hit pattern. The miss rate will be 50%.

Question d. An array of long with 8 rows and 128 columns, a two-way set-associative cache with LRU replacement, and the function sumB from the program cache-test provided in the first part of the assignment.

Answer d. Since it's a two-way set-associative cache, that means that we have 16 sets (32 blocks / 2) with two blocks in each of them. As mentioned before, sumB access elements in a column-major order. Since the number of columns is divisible by the number of sets, that means that the elements in the same row will be saved in the same set. As given by the question, the replacement policy is LRU, when we request the data for the next column, it will have been replaced, so we are going to get a miss every time. The miss rate is 100%.

Question e. An array of long with 8 rows and 128 columns, a four-way set-associative cache with LRU replacement, and the function sumB from the program cache-test provided in the first part of the assignment.

Answer e. Since it's a four-way set-associate cache, we will have 8 sets with 4 blocks in each of them. It allows us to reduce the miss rate. The number of columns is once again divisible by the number of sets, indicating that similar to Question d, the elements that are in the same row will be stored in the same set. Having more blocks in a set allows us to "postpone" the replacement of the data used for the new one, because when we access the  next column we still have access to the previous row, allowing us to have 12.5% miss rate.

Question f. An array of long with 8 rows and 128 columns, a four-way set-associative cache with random replacement, and the function sumB from the program cache-test provided in the first part of the assignment.

Answer f.

Question g. An array of long with 8 rows and 120 columns, a direct-mapped cache, and the function sumB from the program cache-test provided in the first part of the assignment.

Answer g.



Part 3, optimization

Change Log:


0. Original base_mask()
The base implementation took:
	Best   :      1898684 usec
	Average:      1951273 usec

1. Make the initialization of the new image work in row-major order. It will decrease the miss rate since our cache works in row-major order. 
The optimized implementation took:
	Best   :      1755183 usec (ratio: 0.932351)
	Average:      1770124 usec (ratio: 0.934864)

2. Change the other loops to row-major order when possible. The same rationale as for change 1.
The optimized implementation took:
	Best   :       254885 usec (ratio: 0.139282)
	Average:       255040 usec (ratio: 0.139129)

Modification number  | Execution time  | Ratio
0		     |	1951273 usec   |  N/A
1		     |	1770124 usec   |  0.93
2		     |	255040 usec    |  0.139

