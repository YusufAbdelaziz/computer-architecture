# CH4 - Cache Memory

- Introduction.
    - Memory is considered to show the widest range of technology, cost organization, performance, and types than any other feature in a computer system.
    - Since there's no single technology to satisfy the memory requirements in a computer system, therefore a computer system is equipped with a hierarchy of memory subsystems either internal (close to processor) or external (using I/O modules).
- Key Characteristics of Computer Memory Systems.
    
    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled.png)
    
    - What is a word?
        - A word is the natural unit of data used by a particular processor design. A word size should be specified. For example 16, 32, 64, and so on.
    - What does location mean in the previous figure ?
        - It means whether a memory is internal or external.
        - What is an internal memory?
            - An internal memory is often equated with main memory.
            - But there're other forms of internal memory such as registers that a processor requires and the control unit also requires its own memory. (Both of these are discussed in later chapters).
            - Cache is also another form of internal memory.
            - What is a control unit ?
                - A control unit is responsible of controlling the CPU hence the whole computer system.
        - What is external memory?
            - An external memory consists of peripheral storage devices such as disk or tape that are accessible to the processor via I/O controllers.
    - Define how to express for capacity for internal and external memories ?
        - For internal memory, capacity is typically expressed in terms of bytes (1 byte = 8 bits) or words (8, 16, 32 bits).
        - External memory is expressed in bytes.
    - Explain the unit of transfer.
        - For internal memory, the unit of transfer is the number of electrical lines into and out of the memory module.
        - This may be equal to the word length but it's often larger such as 64, 128, or 256 bits.
    - Define a word, addressable units, and unit of transfer.
        - Three important related concepts for internal memory
            
            
            | Word | Addressable units. | Unit of Transfer |
            | --- | --- | --- |
            | * As defined previously, word is the natural unit of data used by a particular processor design | In some systems, addressable units are the words. Many systems allow addressing at the byte level. | For main memory, unit of transfer is the number of bits read out of or written into memory at a time. It's not equal to a word or an addressable unit. |
            | * The size of a word is equal to the number of bits used to represent an integer and to the instruction length. |  | For external memory, data are often transferred as blocks (much larger units than word) |
    - List different access methods.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%201.png)
        
        - Note that a shared memory is a memory that is being access simultaneously by multiple programs with an intent to provide communications among these programs and to avoid redundant copies.
        - For more info, check this table.
            
            
            | Sequential Access | Direct Access | Random Access | Associative |
            | --- | --- | --- | --- |
            | Memory is organized into units of data, called records.
            Access must be made in a specific linear sequence. Stored addressing information is used to separate records and assist in the retrieval process. A shared
            read–write mechanism is used, and this must be moved from its current location to the desired location, passing and rejecting each intermediate record. Thus, the time to access an arbitrary record is highly variable. Tape units, discussed
            in Chapter 6, are sequential access. |  As with sequential access, direct access involves a shared read–write mechanism. However, individual blocks or records have a unique address based on physical location. Access is accomplished by direct access to reach a general vicinity plus sequential searching, counting, or waiting to reach the final location. Again, access time is variable.  | Each addressable location in memory has a unique, physically wired-in addressing mechanism. The time to access a given location is independent of the sequence of prior accesses and is constant. Thus, any location can be selected at random and directly addressed and accessed. Main memory and some cache systems are random access. | This is a random access type of memory that enables one to make a comparison of desired bit locations within a word for a specified match, and to do this for all words simultaneously. Thus, a word is retrieved based on a portion of its contents rather than its address. As with ordinary random-access memory, each location has its own addressing mechanism, and retrieval time is constant independent of location or prior access patterns. Cache memories
            may employ associative access. |
    - List the three performance parameters.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%202.png)
        
        - So what does the recovery actually mean ?
        - The main memory uses capacitors to store data (to be discussed later at main memory chapter), if the capacitor is charged then we’re storing 1, and if it’s uncharged then we’re storing 0.
        - But we already know that in an ideal capacitor, it can maintain the charge for an infinite amount of time. In reality, ideal capacitors don’t exist, so there’s a possibility of losing the charge, which leads to uncertainty whether the capacitor was initially charged or uncharged.
        - A recovery must be done, this happens via adding a threshold value for the capacitor charge, when the capacitor is discharging and thus passing over the threshold value, we’d do a recovery to reduce the uncertainty.
    - Discuss the most common forms of a memory.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%203.png)
        
    - Discuss the most important physical characteristics of data storage.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%204.png)
        
- Design constraints and different trade-offs to be considered.
    
    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%205.png)
    
- Memory Hierarchy, locality, and hit and miss.
    
    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%206.png)
    
    - As you go down the hierarchy, the following occurs:
        - Decreasing cost per bit.
        - Increasing capacity.
        - Increasing access time.
        - Decreasing frequency of access of the memory by the processor due to a principle called **locality**.
    - Cache is like a middleman memory between the main memory and the processor registers used to staging the movement of data between them to improve performance.
    - Since processors are getting faster in a fashion that main memory can't keep up with, a cache (which is memory) is a subset of the main memory.
    - So what are **hit and** **miss**?
        - A **hit** is when a processor asks for a data and it finds that data in the cache without retrieving it from main memory.
        - A **miss** is when a processor doesn't find the data it wants from the cache, thus the cache has to replace its contents with the required data by the processor. Replacement algorithms are discussed in detail later in this chapter.
    - What is locality ?
        - Locality is when a program tends to use data and instructions with addresses near or equal to those they have used recently.
        - Locality is divided into two types.
            - Temporal locality : which is recently referenced items are likely to be referenced again in the near future.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%207.png)
                
            - Spatial locality : which is items with nearby addresses tend to be referenced in near future.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%208.png)
                
            
    - How do caches take advantage of this?
        - In temporal locality, cache just stores the last reference so that it has the ability to visit it once again.
        - In spatial locality, you retrieve an entire block of memory, for example, say that you've retrieved a memory slot called A, since you retrieve the whole block, you get A+1, A+2, ...etc, until a certain limit.
    - Example of locality.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%209.png)
        
        In this example, define where does locality exist.
        
        - Solution
            - Data
                1. Temporal : sum referenced in each iteration.
                2. Spatial : array a[] accesses in stride-1 pattern (stride here means step, since when we access the memory sequentially, we increment i by 1).
            - Instructions
                1. Temporal : the loop cycle is retrieved from the same reference each time.
                2. Spatial : references to instructions in sequence, (retrieving an item, incrementing a variable for example) which need to be stored near each other to be accessed sequentially.
    - Performance of two-level memory and access time.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2010.png)
        
        - Suppose that the processor has access to two levels of memory. Level
        1 contains 1000 words and has an access time of 0.01 μs; level 2 contains 100,000 words
        and has an access time of 0.1 μs. Assume that if a word to be accessed is in level 1, then the
        processor accesses it directly. If it is in level 2, then the word is first transferred to level 1
        and then accessed by the processor. For simplicity, we ignore the time required for the processor
        to determine whether the word is in level 1 or level 2. Figure 4.2 shows the general
        shape of the curve that covers this situation. The figure shows the average access time to
        a two-level memory as a function of the hit ratio H, where H is defined as the fraction of
        all memory accesses that are found in the faster memory (e.g., the cache), T1 is the access
        time to level 1, and T2 is the access time to level 2. As can be seen, for high percentages
        of level 1 access, the average total access time is much closer to that of level 1 than that
        of level 2.
        - In our example, suppose 95% of the memory accesses are found in level 1. Then the
        average time to access a word can be expressed as
            
            (0.95)(0.01 μs) + (0.05)(0.01 μs + 0.1 μs) = 0.0095 + 0.0055 = 0.015 μs
            
            The average access time is much closer to 0.01 μs than to 0.1 μs, as desired.
            
        - Accordingly, it is possible to organize data across the hierarchy such that the
        percentage of accesses to each successively lower level is substantially less than that
        of the level above. Consider the two-level example already presented. Let level 2
        memory contains all program instructions and data. The current clusters can be
        temporarily placed in level 1. From time to time, one of the clusters in level 1 will
        have to be swapped back to level 2 to make room for a new cluster coming in to
        level 1. On average, however, most references will be to instructions and data contained
        in level 1.
        - This principle can be applied across more than two levels of memory, as suggested
        by the memory hierarchy. The fastest, smallest, and most expensive
        type of memory consists of the registers internal to the processor. Typically, a
        processor will contain a few dozen such registers, although some machines contain
        hundreds of registers. Main memory is the principal internal memory system of
        the computer. Each location in main memory has a unique address. Main memory
        is usually extended with a higher-speed, smaller cache. The cache is not usually
        visible to the programmer or, indeed, to the processor. It is a device for staging
        the movement of data between main memory and processor registers to improve
        performance.
- What is a disk cache?
    - Disk cache is a **portion of the main memory** used as a buffer to hold data temporarily.
    - It improves the performance in two ways:
        1. A few large transfers of data can be used instead of many small transfers of data which reduces processor involvement.
        2. Data can be fetched rapidly from the software cache rather than slowly from the disk
- Cache and main memory organization.
    
    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2011.png)
    
    - Figure 4.3a illustrates the idea of the cache and memory. Cache is faster and smaller memory combined with relatively larger and slower main memory. When a processor tries to read a word of memory, a check happens to determine whether the word is in the cache. If the data exists, then give it back to the processor, if it's not, get it from the main memory.
    - Due to the principle of locality of reference, when a block of data is fetched into the cache to satisfy a single memory reference, it's more likely that there'll be future references to the same memory location (temporal locality) or other words in the block (spatial locality).
    - Figure 4.3b illustrates the use of multi-level cache in which L3 < L2 < L1 wrt speed and L1 < L2 < L3 wrt capacity.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2012.png)
        
    - Main Memory structure.
        - As shown in the figure, main memory consists of $2^n$ addressable words, with each word has $n$-bit unique address.
        - For mapping purposes, the main memory is divided into a fixed-length blocks of $K$ words each.
        - There are M blocks and the number of blocks in main memory is
            
            $$
            M = \frac{2^n}{K}
            $$
            
    - Cache Structure.
        - The cache consists of $m$ blocks, called lines (To differentiate it from a main memory block and the cache line includes K words of data, tag, and control bits. The last two don't exist in main memory so a different terminology is necessary).
        - A line consists of **K words of data**, plus a few bits for **a tag**, and **control bits** to indicate whether the line has been modified since being loaded into the cache.
        - The line size is the length of a line not including the tag and control bits.
        - The number of lines is considerably less than number of blocks as the lines are subsets of main memory blocks.
        - Since a block of main memory cannot be stored in a line, a word from the block is transferred from main memory to one of the lines of the cache and a **tag** is used to identify which particular block is currently being stored.
- Cache organization.
    
    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2013.png)
    
    - As you can see, the processor is connected to the cache via control, address, and data lines. The data and address lines are attached to the data and address buffers respectively which both of them are attached to a system bus from which main memory is reached.
    - When data hit occurs, the data and address buffers are disabled and both the cache and the processor are connected.
    - When data miss occurs, the desired address that was is required from the processor is loaded on the system buss and the data are returned through data buffer which passes the data to both the processor and the cache.
    - In other organizations, cache may be physically interposed between the processor and the main memory for all address, data, and control lines. In that case when data miss occurs, the data is first read into the cache and then the processor gets the data from the cache.
- Elements of cache design.
    - Basic design elements are illustrated below.
    
    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2014.png)
    
    - Cache addresses
        - Most of nonembedded processors and many embedded processor supports **virtual memory**.
        - A virtual memory is a facility that allows a program to address memory from a logical point of view without considering the physical amount of main memory remaining.
        - We used an MMU (memory management tool) to translate the virtual address which is stored in a machine instruction to a physical one.
        - A system designer has two options:
            1. Put the cache between the processor and the MMU, and thus our cache is called a **logical** or **virtual cache**.
            2. Place the cache between MMU and main memory, thus our cache is called **physical cache** which stores physical addresses from main memory.
        - First approach has an advantage that the processor can fetch data from the cache faster than translating the virtual address and after that fetching data from the cache.
        - But it has a disadvantage as all program applications would have the same virtual memory (which usually starts at address 0) which requires the cache memory to be completely flushed for each application context (means that the cache should dedicate itself for each application separately), or you may add extra bits to each line of the cache to identify which virtual address space this address refers to.
        - Hey, do you have extra time ? [check this video](https://www.youtube.com/watch?v=qlH4-oHnBb8&ab_channel=DavidBlack-Schaffer).
        - Note : Virtual memory is revisited in detail in chapter 6.
        
    - Cache size
        - We should try until we find a proper cache size.
        - The size of a cache should be small enough so that the overall average cost per bit is close to that of main memory alone and large enough so that the overall average access time is close to that of the cache alone.
        - The larger the cache, the larger the number of gates which results in slower cache than the smaller ones.
    - Mapping function.
        - Since the cache lines are fewer than main memory blocks, an algorithm is needed to determine which main memory block occupies a cache line.
        - The choice of map function (the algorithm) determines the cache organization.
        - Direct mapping.
            - Each block of main memory is mapped into a unique line in the cache. The mapping can be expressed as $i = j \space modulo\space m$ (round-robin) such that  $i$ is the line number, j is the block number, and m is the number of lines.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2015.png)
                
            - An illustrative example.
                - Suppose you have a memory size of 64 words, and the block size is 4 words, hence the number of blocks is 64/4 which is 16 blocks.
                - You need 2 bits to address each word in your block.
                    
                    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2016.png)
                    
                - Okay now I want to address a word in the memory, how many addressable bits do I need ? You need 6 bits ( $log_2(64) = 6$ ). The 6 bits are called physical address or P.A for short. So first we may need to access the block and then navigate to the word we want. Since we have 16 block, we need 4 bits to find our block, and more 2 bits to find the word in that block, So the most significant bits in the address which are 4 bits are used to identify the block, and the LSB bits which are 2 bits are used to identify the word inside the block.
                - Now our cache size is 16 words, and the line size is 4 words (it’s the same as the block size) so we have 4 lines in our cache, each line storing a block taken from the main memory.
                - Now here comes the problem, how the heck would we store 16 block into 4 lines ? round-robin comes to rescue (the modulo operator).
                - So we may map the first block of the main memory to the first line, the second block to the second line and so on.
                    
                    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2017.png)
                    
                - Now our lines in the cache are all occupied, to store the block number 4 for example, we need to replace it with the line number 0, and so on in a round-robin manner.
                - We may notice that the first line can be mapped to the block numbers 0, 4, 8, 12. You may notice that their binary equivalent representation starts with 00 as LSB. But how will we know which block of these four is stored in the line ? the **tag** comes to rescue !.
                - Tag is used to know which block of the 4 blocks that might be mapped to our line is stored inside that line.
                    
                    ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2018.png)
                    
                - So now your physical address is now divided into three parts or fields. We first want to know the correct block so we have a block number. In the block number, we want to know two things, which block is mapped to which line using the line number field and whether the block we have in the cache is the same as the block we want using the tag field. Lastly, the word field is used to select which word we want to retrieve from the block.
                - You may notice the biggest disadvantage is that the each block must be mapped to a specific line in the cache. So let’s say we’re accessing the block number 0 in the main memory so it’s now stored in the cache line number 0. It happens that we may want the block number 4 which results in replacement of the block number 0 we stored before in line number 0. The issue comes when we want to access the block number 0 again. So we’re going to make a lot of replacements over here.
            - For caching purposes, the main memory is divided into three fields. The LSB (Least Significant bit) which may be symbolized as $w$ which denotes the **word number** in a block, the remaining $s$ bits (the tag and line bits combined) specify one of the $2^s$ blocks of main memory. As illustrated below, suppose you have 24-bits memory address, the 14-bit **line** number is used as an index to the cache to access a particular line. If the 8-bit tag in the main memory matches the 8-bit tag in the cache, the last 2-bit word is used to pick one of 4 bytes (the desired word number) in that line. If tags don't match, then the 22-bits are used to fetch a block from main memory, and the last 2-bits are reset to 0.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2019.png)
                
            - So in our first example, we have 4 words for each block so we need only 2 bits to address the word number in a block.
            - A tag is used for naming purpose, so to distinguish which data come from which blocks. A line may store any block in the memory, but we need to make sure that our line is equivalent to the block we’re looking for, thus **tag** helps us to make the matching process.
            - The $s$ bits are interpreted by cache logic into a **tag** and a **line** field, a line field is $r$ bits, therefore the tag is $(s-r)$ bits (MSB). So the number of lines in cache is $2^r$.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2020.png)
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2021.png)
                
            - For more clarification, check [this video](https://www.youtube.com/watch?v=V_QS1HzJ8Bc&ab_channel=NesoAcademy).
            - The advantage of using direct mapping is that it's easy to implement and inexpensive.
            - The biggest disadvantage is the fixed cache location for any given block. So if a program happens to reference two different words from different blocks that maps to the same line number repeatedly, then the blocks would be swapped continually in the cache which results in low hit ratio (thrashing).
            - To overcome such problem, you may use a **victim cache** which remembers what was discarded in our cache in case we needed previously stored data once more.
            - A victim cache is fully associative cache that resides between a direct mapped L1 cache and the next level of memory.
            
        - Associative Mapping.
            - In this type of mapping, each MM block may be loaded to any line in the cache, therefore overcoming the direct mapping disadvantage.
            - The control logic in the cache interprets the memory address as two fields, which are **the tag** and **the word**.
            - The tag is used to identify a MM block, so a matching takes place to find a correct line's tag.
            - Since there's no field for line number in address format (only a tag and a word), we can't find the number of lines in a cache.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2022.png)
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2023.png)
                
            - The principal disadvantage of this mapping method is the complex circuity, hence hit latency, because you need to add a comparator circuit to compare between MM's block tag and a line's tag.
        - Set-Associative Mapping.
            - This type of mapping exhibits the strengths of both the direct and associative mapping while reducing their disadvantage.
            - In this method, we divide the cache into number of sets, each has a number of lines. The relationships are :
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2024.png)
                
            - Each word in a block can map to any cache line in a specific set.
            - You can physically implement a set-associative cache in two ways :
                1. v associative cache.
                    - In v associative cache, each block maps into a specific set, so for example $B_0$ maps to set 0 and so on. This type is used for high degrees of associativity
                        
                        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2025.png)
                        
                2. k direct mapping cache.
                    - In k direct mapping cache, each direct mapped cache is referred to as a **way** (basically you're having a horizontal sets rather than the vertical ones) which contains $v$ lines. So for the figure below, the first $v$ lines of memory are direct-mapped into the v lines of each way. This type is used for small degrees of associativity.
                        
                        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2026.png)
                        
            - In this type of mapping, the cache control logic interprets each MM address as three fields : **Tag**, **Set**, and **Word.**
            - The d set bits specify one of the sets, the number of sets is $v = 2^d$. Whereas the $s$ bits of **Tag** and **Set** fields specify one of the $2^s$ blocks of main memory.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2027.png)
                
            - The advantage is that tag comparison is reduced since you need to know the the correct set using set bits and thereafter you can start comparing the MM block's tag with the cache's line tag.
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2028.png)
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2029.png)
                
                ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2030.png)
                
            
            - Notice that you have two extremes, the first is the each set in your cache has only one line ( $v = m,\space k = 1$) which is direct mapping.
            - The second is that the whole cache is a single set ($v = 1, \space k = m$) which is associative mapping.
            - The most common form of set-associative is two lines per set ($v = \frac{m}{2}, \space k = 2$) as it improves the hit ratio over direct mapping significantly.
            
            ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2031.png)
            
            ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2032.png)
            
    - Replacement Algorithms.
        - When a processor needs data from a cache and it doesn't find that data, the data is retrieved from the MM and then one block of caches is replaced with the new data.
        - In **direct mapping**, each block in MM has a specific or one possible line in the cache, therefore no replacement algorithm is needed.
        - In **associative** and **set-associative**, each block in the MM can be mapped to any line in the cache, therefore a replacement algorithm is needed.
        - To achieve high speed, a hardware implementation for an algorithm is used. LRU is considered to be the most effective algorithm in our list.
        
        | Least Recently Used (LRU) ⚡ | First in First out (FIFO)  | Least Frequently Used (LFU) | Random |
        | --- | --- | --- | --- |
        | * Replace that block in the set that has been in the cache longest with no reference to it.  | * Replace that block in the set that has been to the cache longest. | * Replace that block in the set that has experienced the fewest references. | * Replace that block in a set randomly without caring about the usage as the previous three types. |
        | * For a two-way set associative, you may have a USE bit to indicate which block in a set is recently referenced. For a the block we just referenced, we may set its USE bit to 1 and set the USE bit of the other block to 0. When replacement happens, the block with USE bit 0 is kicked out of the set and replaced with another one from the MM. | * FIFO is easily implemented as a round-robin or circular buffer technique. | * LFU can be implemented be associating a counter with each line. |  |
        | * As we assume that most recently used memory locations are more likely to be referenced in the near future, LRU should give the best hit ratio. |  |  |  |
        | * In a fully associative cache, a separate list is used for indexing purpose such that the line that is recently referenced is moved to  the head of that list whereas the line at the back of the list is used for replacement. |  |  |  |
        - Simulation studies have shown that replacing the blocks randomly has the least performance among the other three algorithms.
    - Write Policy
        - When a line in a cache is to be replaced, there're two cases to consider:
            1. That line in the cache is not altered, hence you may replace it with a new block coming from MM.
            2. One word in that line is altered, therefore that update must be written out to its equivalent block in the MM.
            
        - A **writing policy** is used to define the way of updating the MM when a line of cache has been altered.
        - The two problems that we may face are :
            1. When more than one device may have access to MM, like I/O module, which have the ability to read or write directly to MM. If a word in a line of the cache is altered, then its corresponding word in MM would be invalid.
            2. When you have multiple processor that are attached to the same bus and each one of them has its own cache. If one word is altered in one cache, then that word becomes invalid in other caches.
            
        - We'll discuss two writing policies, which are :
            1. **Write through** which is considered to be the simplest writing technique. In this technique, all writes operations are made to main memory as well as to the cache to ensure consistency. In the second problem discussed earlier, each processer may monitor traffic to main memory for consistency. The main con of this technique is the substantial memory traffic which leads to bottleneck.
            2. **Write back** which minimizes memory writes. In this technique, updates only happen in the cache and each line has a **dirty** or **use bit.** When an update happens, that bit is set. So in block replacement, this block is written back to the memory if the use bit is set to 1. The main disadvantage is that some portions of MM are invalid, hence I/O modules have to access the cache which results in complex circuitry and a potential bottleneck. 
        - Bus organization and cache coherency.
            
            ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2033.png)
            
    - Line Size
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2034.png)
        
    - Number of Caches and Split vs. Unified caches.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2035.png)
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2036.png)
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2037.png)
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2038.png)
        
    - For more info, read Pentium 4 cache organization.
        
        ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2039.png)
        
        - Instruction fetch/decode unit is used to produce micro instructions that are passed to the L1 instruction cache.
        - Out-of-order execution logic is responsible of observing whether a set of instructions are dependent on each other or not. If they are dependent, then execute these instruction sequentially, otherwise try to execute these instruction parallelly.
            
            ![Untitled](CH4%20-%20Cache%20Memory%20b64748f6973e420abf4094f2bca1476b/Untitled%2040.png)