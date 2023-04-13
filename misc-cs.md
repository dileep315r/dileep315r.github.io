#### Miscellaneous
1. A memory-mapped file is a segment of virtual memory[1] that has been assigned a direct byte-for-byte correlation with some portion of a file or file-like resource. This resource is typically a file that is physically present on disk, but can also be a device, shared memory object, or other resource that the operating system can reference through a file descriptor. Once present, this correlation between the file and the memory space permits applications to treat the mapped portion as if it were primary memory.
   1. Accessing memory mapped files is faster than using direct read and write operations for two reasons. Firstly, a system call is orders of magnitude slower than a simple change to a program's local memory. Secondly, in most operating systems the memory region mapped actually is the kernel's page cache (file cache), meaning that no copies need to be created in user space.
   2. I think this feature is used to speed up processing in Kafka.
   3. Page fault handing mechanism similar mechanism is used for memory-mapped files, which are mapped to virtual memory and loaded to physical memory on demand.
2. https://en.wikipedia.org/wiki/Page_table for paging
   1. Address translation: virtual address --> CPU TLB cache --> page table in memory
   2. Look up page: virtual address --> CPU TLB cache -->  CPU cache lookup --> load page from memory or disk
   3. Good stackoverflow answers
      1. https://stackoverflow.com/questions/37825859/cache-miss-a-tlb-miss-and-page-fault
      2. https://stackoverflow.com/questions/218117/how-cache-memory-works
      3. https://stackoverflow.com/questions/10116033/heap-memory-and-slab-allocation
3. Segmentation
   1. Address coming out of CPU contains segment id and offset. Every segment lives in it's own virtual memory.
   2. Data/symbol_table and other sections in the contiguous virtual memory layout may overflow. Segmentation provides an easy way to increase size of different sections.
   3. Segmentation makes sharing of shared libraries easy.
   4. Hardware prevents execution of non-code/non-executable sections.
4. See [link](https://security.stackexchange.com/questions/129098/what-is-protection-ring-1/129103#129103) for privilege levels and privileged instructions on hardware.
5. See [link](https://security.stackexchange.com/questions/175789/does-the-main-os-run-virtualised-under-the-ring-1-hypervisor) to know how the hardware virtualization works.
6. See [link](https://www.intel.in/content/www/in/en/gaming/resources/hyper-threading.html) for 1vCPU, CPU threads concept.
7. SSD [write amplification](https://en.wikipedia.org/wiki/Write_amplification). Flash memory must be erased before it can be rewritten. Thus, rewriting some data requires an already-used-portion of flash to be read, updated, and written to a new location, together with initially erasing the new location if it was previously used. Due to the way flash works, much larger portions of flash must be erased and rewritten than actually required by the amount of new data. This multiplying effect increases the number of writes required over the life of the SSD, which shortens the time it can operate reliably. 
8. Gunther's law of multiprogramming: The maximum throughput of a system is proportional to the number of concurrent activities, and is limited by the number of resources available.
   ![img](https://i0.wp.com/blog.knoldus.com/wp-content/uploads/2019/01/scalability_laws_of_scalability.jpg?w=371&ssl=1)
9. [Amdahl's law](https://en.wikipedia.org/wiki/Amdahl%27s_law)
   ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/AmdahlsLaw.svg/1200px-AmdahlsLaw.svg.png)
