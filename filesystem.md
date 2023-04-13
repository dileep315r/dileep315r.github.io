#### File system

### File memory allocation

#### Free list maintenance
1. Linked list of free blocks.
   1. Takes a lot of space compared to bitmap approach.
2. Bitmap
   1. Inefficient if the disk is almost full. Requires reading > 10 blocks.

#### Allocation types
1. Contiguous blocks.
   1. Don't know the file size beforehand
   2. Leads to fragmentation of the disk space.
2. Linked list of blocks for the file. Add new block to the end of the list. Each block first few bytes point to the next data block. 
   1. Random access is inefficient.
   2. Block doesn't hold power of two memory.
3. Global table/map of block numbers to next block number of files. Used in MS-DOS. Global table is kept in memory.
   1. High memory overhead.
   2. Not efficient for random access.
4. I-node(i.e Index node). i-node contains addresses of the blocks, pointer to single level block pointers, pointer to two level block pointers, pointer to three level block pointers.
   1. Random access is efficient.
   2. At least two disk block reads are required to read one block of data.
   3. Store i-nodes in the middle track to reduce the disk seek latency. Alternatively, store i-nodes of a cylinder group together in the cylinder.

#### Directory data storage
Directory is a file, and it contains info about its files.
1. Directory entry contains file meta data.
   1. Store file attributes and the initial block number of the file in the directory entry.
      1. Applicable for linked list allocation and global table allocation.
2. Directory entry doesn't contain file metadata.
   1. Directory entry contains file name and i-node number, inode contains file metadata.

#### Performance improvement
1. File systems try to store the frequently accessed together i.e consecutive file blocks closer.
   1. Store the file blocks in the same cylinder.
2. Cache frequently accessed blocks in RAM. Write through or write back to send data to disk.
3. Log structured file system
   1. Assumes that the reads are served mostly from RAM and writes are synced to disk.
   2. Accumulate writes to a segment in RAM and append the segment to filesystem.
   3. Compact old segments. Delete deleted disk blocks.

#### Consistency
OS kernel reads, modifies and updates the file system datastructures. System might crash in between the read-modify-write cycle.
1. OS automatically checks for filesystem consistency during booting.
2. Information about the file system data structures is maintained in separate blocks to check for the consistency.
   1. Store number of free blocks
   2. Store number of used blocks
3. Journaling file system:
   1. Write the changes to the disk before executing the change.
   2. System will recover from the journal after restart.

### Ideal block size
1KB based on the research statistics for data rate vs disk utilization vs block size. Refer Tanenbaum OS book.

### Security
Store encrypted "password + salt" string to the passwords file. Salt is used to avoid the precomputed encrypted password lookup attack.

#### ACL
1. Map of linked lists. Each entry in the map stores the access/auth control information of a resource.
2. Each item in the linked list stores the authorization information of an identity.
3. ACL is an alternative to the matrix representation. ACL is efficient over matrix representation as the matrix is generally sparse.

#### Capability lists
1. Other way of storing the authorization information.
2. Map of user id to user's capabilities.

Linux file system directory purpose given in https://www.youtube.com/watch?v=A3G-3hp88mo
1. /dev - devices
2. /home
3. /boot
4. /usr/bin /usr/sbin contains binaries for the linux commands
5. /lib - shared libraries
6. /var - log files and web application files
7. /root home for root
8. /bin - linux command binaries
9. /etc - all the configurations of system and some applications
10. /media - system mounting things automatically for you
11. /mnt - manually mounted files
