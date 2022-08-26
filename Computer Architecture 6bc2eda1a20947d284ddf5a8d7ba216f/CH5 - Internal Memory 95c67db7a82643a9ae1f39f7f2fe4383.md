# CH5 - Internal Memory.

- How to identify whether a memory is internal or external ?
    - When a set of memories is communicating in the same manner, they’re said to be internal.
    - For example, in registers or caches we read and write using electrical signals.
    - So the same signals we use to do mathematical operations in the processor, is the same signal we use to read from or write to the register/cache/main memory.
    - In case of hard drives (external memory), there’s a intermediary circuit that takes in the electrical signal that is sent by the processor and produce a magnetized sectors on the drive.
    - So basically if your memory needs a intermediary circuit (controller) for communication, then it’s an external memory.
    - And if it’s directly connected to the buses, then it’s internal.
    - But how about SSDs ? they’re writing/reading electrically right?
    - Yes they’re, but they still need to interact with an interface (control circuit) because it’s placed in the same slot as hard disk so it has to use the same interface.
- Semiconductor memory.
    - It’s a type of memory in which we use gates (flip-flops) to store data.
    - The following table divides the semiconductor memory into two types, RAM and ROM (with its various types).
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled.png)
        
    
    - In RAM, we use electricity to operate the read-write mechanism. Once there’s no electricity, the data vanishes.
    - In ROM, the data are burnt into the memory by the manufacturer. While in the PROM, you can write or burn the data into the memory by using an interface or software, but you still can’t rewrite on the memory.
    - The third category is the read-mostly memory. It’s a kind of memory that you can write but most likely you’re going to read from it.
    - The first kind is EPROM, in which you can write on the memory in the same way you write with PROM but you can only erase on the chip-level which means the whole data are cleared unlike the RAM where you can erase on the byte-level. The chip must be detached and placed under UV light for about 20 minutes which results in erasing all data.
    - The EEPROM is similar to the RAM, as you can electrically erase the data on the byte-level.
    - So since EEPROM is similar to RAM, why can’t we just replace the RAM with EEPROM ?
    - The main reason is that write operations are slower compared to RAM, as you can see, the EEPROM is a read-mostly memory.
    - The flash memory is the last type that is fast but you can only erase on the block level, similar to hard disk in which you can erase each sector.
    
- Forms of RAM.
    - Dynamic RAM (DRAM).
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%201.png)
        
        - Each cell in the memory consists of one capacitor and one transistor (nMOS).
        - When the address line is active (value set is 1) then the transistor is a short circuit, so whatever on the bit line (B) is transmitted to the capacitor.
        - When the address line is inactive (value set to 0) then the transistor is an open circuit, thus if the capacitor is charged (which mean stores 1) then it’ll remain with that charge.
        - The main disadvantage is that the charge stored in the capacitor is dissipated over time.
        - When the charge decreases (say from 1V to 0.9V), we need a threshold value that is interpreted as 1V or 0V. Say your threshold value is 0.5 V, then if your capacitor is charged with 0.4V, then the refreshment circuit would consider that the capacitor has a noise charge and starts to discharge the capacitor to make it empty.
        - The refreshment circuit is responsible of checking for each cell in the memory, and decides to charge and discharge each cell in the memory depending on the threshold value.
        - So you can deduce that another disadvantage is that you can’t read from the memory while the refreshment or recovery operation is still in progress.
        - Another disadvantage is that there’s a time spent on charging and discharging the capacitor.
        - Advantages
            - Cheap, you only need a capacitor and a transistor.
            - Small space for each cell.
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%202.png)
        
    - Static RAM (SRAM).
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%203.png)
        
        - The previous cell depicts a SRAM cell.
        - If we activate the transistor $T_1$, then the transistor $T_3$ is deactivated. The same goes with $T_2$ and $T_4$.
        - Now let’s check $T_5$ and $T_6$. When both are activated (the value set on them is 1 coming from address line) then whatever is passed from the bit line is reached to the points $C_1$ and $C_2$.
        - You can notice from the structure that $T_3$ and $T_4$ are connected to the $V_{cc}$, and $T_5$ and $T_6$ are both connected to the address line. Also $T_1$ and $T_2$ are connected to the ground.
        - How to store 1 or 0 ?
        - Let’s set the bit line to 1, we notice that $T_5$ is activated, hence $C_1$ has the value 1. You can notice that there’s a wire connected to the $T_4$ and $T_2$ branch which would activate $T_2$ and deactivate $T_4.$
        - Let’s go for the other bit line that is set to 0 (the inverted value of 1), we notice that $T_6$ is deactivated, hence the point $C_2$ has the value of 0. This value is therefore passed to the $T_3$ and $T_1$ branch which results in deactivating $T_1$ and activating $T_3$.
        - You may conclude that $C_1$ maintains $C_2$’s value and vice versa.
        - This works the same as a flip-flop works but in the transistor-level.
        - Advantages and disadvantages.
            
            ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%204.png)
            
    - DRAM vs SRAM
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%205.png)
        
- ROM
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%206.png)
    
- ROM types.
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%207.png)
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%208.png)
    
- Memory organization.
    - Say you have a 1 MB memory, how many addressable bits do you need to access a single unit in that memory ?
    - You’d need $20$ bits, as you have $2^{20}$ slots in your memory.
    - But now you have a 2 x 512 KB memory, can we still combine these two memories to operate as a single 1 MB memory ?
    - Yes you can, you may have 19 bits to address a slot, and the 20th bit may be used as a selector bit to select whether the address you asked for exists in the first or the second memory chip.
    - You may use a decoder for selection if you have a lot of memory chips.
    - Various organizations.
        - 16 Mb DRAM organization.
            
            ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%209.png)
            
            - We can divide our 16 Mb DRAM into 4 memory array.
            - Let’s take a single 4 Mb memory array and discuss about it.
            - To represent a 4 Mb memory array, you need a 11 bits to represent the rows and another 11 bits to represent the columns. The row and column decoders are used to select the bit we want when both decoders receive the addresses from the row address and column address buffers respectively. The bit we selected are fed to the output buffer.
            - You can repeat the same process 4 times to get the 16 Mb memory.
            - You may also notice that there’re signals received from above which are RAS, CAS, WE, and OE and they stand for row address select, column address select, write enable, and output enable respectively.
            - So if you pass an address to the CAS, this address is only passed to the column buffer, the same goes with RAS.
            - You may write or read on the bit you want depending on the WE signal.
            - We haven’t discussed about the refresh counter and the MUX.
            - Recall that we mentioned that DRAM has two modes, the first is the read/write mode and the second is the refreshment mode.
            - The use of the MUX is to select between these modes.
            - So you pass the row or the column address to the refresh counter, and starting from these addresses, it refreshes these addresses and all subsequent addresses (the row or the column) till the 2048 bits are all refreshed.
        - 256Kb 8-bit word organization.
            
            ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2010.png)
            
            - In this organization, we have 8 memory chips ( there’re only 3 but just for the sake of brevity ), and each memory chip has 256Kb in size and has 512 bit rows and 512 bit columns, each chip would produce a single bit that is being selected from the MAR, and therefore we’d get the 8-bit word.
            - The same row and column that are selected in one chip, is the same in all chips.
            
        - 1 Mb 8-bit words.
            
            ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2011.png)
            
            - This is almost the same organization as the previous one but we used 4 modules of 256Kb memory.
            - We still need 9 bits to address the row, and another 9 bits to address the column, but how would we select which bit should come out from which module ?
            - Since we have 4 modules, we need 2 bits to address each module separately.
- Error Correction
    - Sources of errors.
        - The first is **hard failure** which is a permanent defect in your memory.
        - The second is the **soft error** which happens randomly, and it’s non-destructive. There’s also no permanent damage to the memory. Some huge equipment may radiate alpha particles, that may affect electric circuits.
    - An example of error detection is the parity bit, but it doesn’t tell us how to correct the error and how to know which bit is incorrect. The parity bit also can’t detect errors in two bits at the same time.
    - Hamming error correcting code.
        - It’s a method to correct an error that may occur while transmitting bits.
            
            ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2012.png)
            
        
        - In Figure (a), say you have four bits, try to represent these bits as Venn diagram such that each bit is intersected by two regions except the 1 at the middle which resides at the three regions A, B, and C.
        - In Figure (b), try to complete each region with an even number of 1s. For example, you had odd number of 1s in the A region, so you should add 1. In region B, you should add 0 to make your number of 1s even.
        - In figure (c), an error occurred at the bit between region A and C.
        - You can therefore count the number of 1s in each region and correct the flipped bits.
        - A tradeoff happen because we’ve added 3 more bits for the sake of error detection.
            
            ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2013.png)
            
        - So when data are passed to the memory, we store the data and the hamming code generated by the **f** block. When we want to read from the memory, we then extract the data and pass it to the hamming code generator to generate a hamming code to be compared with the hamming code we previously stored. If both are the same, then the data is OK. In case of incorrectness, we use a corrector circuit to correct the messed up bits.
        
- Advanced DRAM Organization.
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2014.png)
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2015.png)
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2016.png)
    
    ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2017.png)
    
- Virtual Memory
    - Virtual memory is used to extend the memory’s space. This is done by transferring the data that the RAM doesn’t work on at the moment to the hard disk.
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2018.png)
        
    
    - The programs that exist in the page file is divided into pages. Each page has a fixed-size blocks. Same structure exist in the main memory.
    - Important terminology
        - **Virtual Address** : The logic address that a process uses.
        - **Physical Address** : The real address in the physical memory.
        - **Mapping** : The mechanism by which virtual address is translated into physical one.
        - **Page frames** : The equal size blocks into which main memory is divided.
        - **Pages** : The blocks into which virtual memory is divided.
        - **Paging** : The process of copying a virtual page from disk to page frame in main memory.
        - **Page fault** : Requested page is not in main memory and must be copied into memory from disk.
        - **Fragmentation** : Unusable space within a given partition (page frame).
    - So to state it clearly, the disk has multiple programs and each one of them is operating in the virtual memory and is divided into pages. If a program is currently in running phase, then the page that exist in the disk is therefore moved to a page frame in the memory.
    - Page Table
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2019.png)
        
        - The page table works as a mapping, it maps the virtual page of the process to its physical one.
        - This table exist with each program, as it determines which page in the virtual memory is mapped to the page frame in the main memory.
    - Paging example.
        
        ![Untitled](CH5%20-%20Internal%20Memory%2095c67db7a82643a9ae1f39f7f2fe4383/Untitled%2020.png)
        
        - The virtual memory is addressable using 8 bits, while the physical memory is addressable using 7 bits. A mechanism is needed to translate the 8 bits that the processor sends to the virtual memory into 7 bits.
        - Dividing the number of words in the virtual memory on the page size, we’d have 8 pages in the virtual memory. Whereas the physical memory has 4 page frames ($2^7 / 2^5 = 4$).
        - So we need to map the 8 pages in the virtual memory to 4 page frames in the main memory.
        - So since we have 32 words, we’d need 5 bits to address each word in the page.
        - So the format of the virtual address would be 5 bits for addressing a word in a page, and 3 bits for addressing one of 8 pages. You can also notice that the 3 bits used to address a page in the virtual memory must be translated into 2 bits to address a page frame in the main memory.
        - You can deduce the importance of the page table. As previously stated, the main use is to know the mapping between the virtual memory and the main memory. For example, the page number 0 is mapped to the page frame number 2.
        - So the processor sends $00001101$ to address a page in the virtual memory, after that we take a look at the page table to see if the this address is already mapped to a main memory’s page frame or not. If it’s not mapped, then we’d go with paging which is mapping or copying the page in the virtual memory into a page frame. If it does exist, then we just access it directly in the main memory which would result in address $101101$