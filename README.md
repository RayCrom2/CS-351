# CS-351
(P.I. = performance improvement)
g-Optimization         |     O2-Optimization         
                  **hash-00**
real    340.18s              real    335.26s              
user    333.49s              user    327.44s              
sys     4.71s                sys     4.64s                
mem (kbytes): 2900           mem (kbytes): 2904           
throughput: 95.7 units/s     throughput: 98.4 units/s     
                  **hash--01**
real    17.79s               real    8.3s                 
user    16.3s                user    6.89s                
sys     1.35s                sys     1.28s                
mem (kbytes): 2900           mem (kbytes): 2896           
throughput: 1826.6 units/s   throughput: 3914.2 units/s 
P.I: 19.1%                   P.I: 40.4%
                  **hash--02**
real    15.77s               real    8.32s                
user    14.22s               user    6.84s                
sys     1.27s                sys     1.33s                
mem (kbytes): 3480           mem (kbytes): 2892           
throughput: 2060.6 units/s   throughput: 3904.8 units/s   
P.I: 21.6%                   P.I: 40.3%
                  **hash--03**
real    16.7s                real    8.21s                
user    15.2s                user    6.79s                
sys     1.18s                sys     1.3s                 
mem (kbytes): 2932           mem (kbytes): 3508           
throughput: 1945.9 units/s   throughput: 3957.1 units/s  
P.I: 20.4%                   P.I: 40.8%
                  **hash--04**
real    14.75s               real    7.36s                
user    13.88s               user    6.65s                
sys     0.57s                sys     .57s                 
mem (kbytes): 5011832        mem (kbytes): 5010096        
throughput: 2203.1 units/s   throughput: 4415.2 units/s   
P.I: 23.1%                   P.I: 45.6%

What operation do you think accounts for most of hash-00's runtime?
- I think the way hash-00 reads the data from an input file one at a time contributes to most of its runtime.
hash-01 and hash-02 both dynamically allocate memory for each hash computation.  Is there much difference time-wise between their two allocation methods?
- The difference between the two is that hash-01 allocates its memory onto the heap while hash-02 puts uses memory from the stack. Performance-wise, hash-02 is always a O(1) operation while
  hash-01is amortized and may be greater than O(1) and has a chance at being further apart resulting in more cache misses.
hash-03 avoids the allocation by using a fixed-size array.  Is there an appreciable speed difference?
- In respect to hash-0, I would say there is an appreciable difference, however, it is not far off from the other methods.
Why is hash-04's memory usage so much larger than any of the other versions?  Hint: recall when we discussed how the operating system reads a file and makes it available to an application.  Specifically, the O/S will transfer data from disk to its own memory, and then copy from there into buffers provided by the application.  In the memory map case, the O/S is merely sharing the copy of the file's data that is in its (the O/S's) memory, and not making an additional copy from its memory into memory only in the application
- It is so much larger because of our ' void* memory = mmap(NULL, size, PROT_READ, MAP_PRIVATE, fd, 0);' command which takes the whole input file and stores it inside the page cache. We can now access it directly without using the input file more than once, but it uses a lot more memory.
What other compiler options did you try, and did they help at all?
- I tried -j4-8 but couldn't get it to work, I also tried -O1 and it seemed to give slightly longer or similar times to -O2. Using -O4, however, did seem to give me consistently faster times tahn both -g and -O2.
