1. A memory-mapped file is a segment of virtual memory[1] that has been assigned a direct byte-for-byte correlation with some portion of a file or file-like resource. This resource is typically a file that is physically present on disk, but can also be a device, shared memory object, or other resource that the operating system can reference through a file descriptor. Once present, this correlation between the file and the memory space permits applications to treat the mapped portion as if it were primary memory.
   1. Accessing memory mapped files is faster than using direct read and write operations for two reasons. Firstly, a system call is orders of magnitude slower than a simple change to a program's local memory. Secondly, in most operating systems the memory region mapped actually is the kernel's page cache (file cache), meaning that no copies need to be created in user space.
   2. I think this feature is used to speed up processing in Kafka.
   3. Page fault handing mechanism similar mechanism is used for memory-mapped files, which are mapped to virtual memory and loaded to physical memory on demand.
2. https://en.wikipedia.org/wiki/Page_table for paging
   1. Address translation: virtual address --> CPU TLB cache --> page table in memory
   2. Look up page: virtual address --> CPU TLB cache -->  CPU cache lookup --> load page from memory or disk
   3. 