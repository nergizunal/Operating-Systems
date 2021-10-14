CS 342 2019 Fall Project 3

Nergiz Ünal 21301027

CODE EXPLANATION
● For this project, to allocate requested size of block, we added a header at the
very beginning of the block itself. This header holds the information about the
size of the block and the address of the next block. More clearly:
struct header
{
int size; → 8 byte
struct header*, next; → 8 byte
}
● In total, header’s size is 16 byte. Since we need to hold 16 byte for each
header, we need to allocate extra 16 additional byte for every requested
block.
● There is also one general header at the beginning of whole memory chunk for
indicating the situation of it.
In app.c, the program allocates 6 blocks with size of (chunksize in kb) *16 byte, for
every allocation method these blocks allocated consecutively. And then the program
frees second, third and fifth blocks.
|----------|----------|----------|----------|----------|----------|-------------------|
Alloc Free Free Alloc Free Alloc Free
And then the program creates 6 threads for allocating memory with size of
(chunksize in kb) *8, this scenario gives different results for every different allocation
algorithms. You can see how these 3 algorithms allocate memory by outputs given
above.EXPERIMENTATION ON DIFFERENT
ALGORITHMS
FIRST FIT:BEST FIT
WORS FITFirst Fit
Best Fit
Worst Fit
time/ #thread 200 150 100 50 30 10
real 0m0.039s 0m0.033s 0m0.024s 0m0.011s 0m0.006s 0m0.005s
user 0m0.005s 0m0.005s 0m0.004s 0m0.000s 0m0.001s 0m0.004s
sys 0m0.028s 0m0.014s 0m0.014s 0m0.010s 0m0.006s 0m0.000s
real 0m0.049s 0m0.039s 0m0.026s 0m0.009s 0m0.008s 0m0.004s
user 0m0.007s 0m0.003s 0m0.004s 0m0.003s 0m0.006s 0m0.000s
sys 0m0.026s 0m0.021s 0m0.011s 0m0.009s 0m0.000s 0m0.003s
real 0m0.039s 0m0.037s 0m0.038s 0m0.008s 0m0.006s 0m0.008s
user 0m0.008s 0m0.005s 0m0.000s 0m0.000s 0m0.000s 0m0.000s
sys 0m0.018s 0m0.017s 0m0.017s 0m0.009s 0m0.007s 0m0.005s
INTERPRETATION OF RESULTS
First fit algorithm is the fastest algorithm among them because it does searching in
less number of time for free space.
Although best fit algorithm has advantage on memory utilization, it has disadvantage
on timing because it searches more.
Last but not the least, worst fit aims reducing the ratio of small gaps, and due to this,
it has similar timing results with first fit
