|Hash #|Optimization|Real Time|User Time|System Time|Memory Usage<br>(KB)|Throughput|Performance<br>Improvement|
|:--:|--:|--:|--:|--:|--:|--:|:--:|
|hash-00|g-Optimization|340.18s|333.49s|4.71s|2900|95.7 units/s|–|
|hash--01|g-Optimization|17.79s|16.3s|1.35s|2900|1826.6 units/s|19.1%|
|hash--02|g-Optimization|15.77s|14.22s|1.27s|3480|2060.6 units/s|21.6%|
|hash--03|g-Optimization|16.7s|15.2s|1.18s|2932|1945.9 units/s|20.4%|
|hash--04|g-Optimization|14.75s|13.88s|0.57s|5011832|2203.1 units/s|23.1%|
|hash-00|O2-Optimization|335.26s|327.44s|4.64s|2904|98.4 units/s|–|
|hash--01|O2-Optimization|8.3s|6.89s|1.28s|2896|3914.2 units/s|40.4%|
|hash--02|O2-Optimization|8.32s|6.84s|1.33s|2892|3904.8 units/s|40.3%|
|hash--03|O2-Optimization|8.21s|6.79s|1.3s|3508|3957.1 units/s|40.8%|
|hash--04|O2-Optimization|7.36s|6.65s|0.57s|5010096|4415.2 units/s|45.6%|

**What operation do you think accounts for most of hash-00's runtime?**
<br>   > I think the way hash-00 reads the data from an input file one at a time contributes to most of its runtime.
hash-01 and hash-02 both dynamically allocate memory for each hash computation.  
**Is there much difference time-wise between their two allocation methods?**
<br>   The difference between the two is that hash-01 allocates its memory onto the heap while hash-02 puts uses memory from the stack. Performance-wise, hash-02 is always a O(1) operation while hash-01 is amortized and may be greater than O(1) and has a chance at being further apart resulting in more cache misses.
hash-03 avoids the allocation by using a fixed-size array.  
**Is there an appreciable speed difference?**
<br>   In respect to hash-0, I would say there is an appreciable difference, however, it is not far off from the other methods.
**Why is hash-04's memory usage so much larger than any of the other versions?  Hint: recall when we discussed how the operating system reads a file and makes it available to an application.  Specifically, the O/S will transfer data from disk to its own memory, and then copy from there into buffers provided by the application.  In the memory map case, the O/S is merely sharing the copy of the file's data that is in its (the O/S's) memory, and not making an additional copy from its memory into memory only in the application**
<br>   It is so much larger because of our ' void* memory = mmap(NULL, size, PROT_READ, MAP_PRIVATE, fd, 0);' command which takes the whole input file and stores it inside the page cache. We can now access it directly without using the input file more than once, but it uses a lot more memory.
**What other compiler options did you try, and did they help at all?**
<br>   I tried -j4-8 but couldn't get it to work, I also tried -O1 and it seemed to give slightly longer or similar times to -O2. Using -O4, however, did seem to give me consistently faster times tahn both -g and -O2.
