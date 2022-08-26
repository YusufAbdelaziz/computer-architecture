# CH11 - Addressing Modes And instruction format.

- Introduction.
    - In the previous chapter, we examined the types of operands and operations that may be specified by machine instructions.
    - In this chapter, we need to know how to specify the operands and operations of instructions.
    - Two questions arise. First, **how to identify the address of an operand**, and second, **how are the bits of an instruction organized to define the operand addresses and operations of that instruction** ?
    - The address field or fields in a typical instruction format is relatively small. Using this small address, we would like to be able to reference a large range of locations in main memory or virtual memory.
    - To achieve this objective, a variety of addressing techniques has been employed. They all involve some trade-off between address range and/or addressing flexibility, on the one hand, and the number of memory references in the instruction and/or the complexity of address calculation, on the other.
    - We have seven common addressing techniques or modes :
        - Immediate.
        - Direct.
        - Indirect.
        - Register.
        - Register indirect.
        - Displacement.
- Addressing Modes.
    - Each address mode has its own merits and demerits, nothing is perfect. A question arises, how would we identify each address mode ?
    - You can basically define a set of operations that work for a specific addressing mode, so different opcodes for different addressing modes.
    - You may also use a **mode field**, so if your architecture supports four addressing modes, you may use 2 bits to represent each one of these modes, but that costs extra space.
    - Before beginning with addressing modes, we need to discuss more about the interpretation of the effective address (EA).
    - **In a system without virtual memory**, the effective address will be either a main memory address or a register.
    - **In a virtual memory system**, the effective address is a virtual address or a register.
    - Recall that the mapping from a virtual address to a physical one is done via memory management unit (MMU) and it’s invisible to the programmer.
    - Effective address is the real address that contains the operand value.
    - Let’s discuss about the addressing modes:
        - Immediate.
            - In this mode, our instruction consists of an operand and opcode.
            - The operand field is value of the data (1, 2, 4, any value), so for example if the instruction was ADD 5, you’d add 5 to the contents of the accumulator (CPU register that has data inside of it) and put the results inside the accumulator.
            - Notice that the execution of the instructions requires no memory reference.
            - It’s relatively fast but with limited range because your adding a constant value (operand) to a variable (data in the accumulator).
                
                ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled.png)
                
        - Direct.
            - In this type, there’s an address field accompanied with the opcode.
            - The address field is the memory address of the operand we want to execute our operation on.
            - So obviously we need a single memory reference to access the data, and execute our operation on the fetched data and the data that resides inside the accumulator.
            - You still have limited range of space, because your address field must have the same number of bits on a memory address.
                
                ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%201.png)
                
        - Indirect.
            - The main idea is that the address field points to a memory cell, and that memory cell has an address of the operand inside the memory.
            - What is the point of that ? You have a wider range of space to use. So if you may have 12 bits of address field that points to a cell in the memory, and that cell may contain larger number of bits, for example, 16 bits.
            - The demerit of this technique is the multiple access to memory to find your operand depending on the number of levels of pointing your using.
            - It’s obviously slower than the previous two techniques.
                
                ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%202.png)
                
        - Register Indirect.
            - Almost identical to the previous except that you store your data pointer address in a register not the memory.
            - So you need two accesses, one for register (which is almost negligible comparing to memory access) and the other for memory access. You can consider it as a single memory access.
                
                ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%203.png)
                
            
        - Displacement.
            - In this type, you have two fields, one for register address and another address called A.
            - The effective address is the addition of the memory address you got from the register plus the address field A. The result of that addition is the operand address in the main memory.
            - Notice that we combined between direct and register indirect addressing modes.
            - So a use case may be referencing array elements, you only need the reference of the first element, and all subsequent elements can be accessed by adding numbers to that reference.
                
                ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%204.png)
                
            - We will describe three of the most common uses of displacement addressing:
                - Relative Addressing.
                    - In this method, the implicitly referenced register is the program counter (PC).
                    - The next instruction is added to the address field **A** to produce the EA. So EA is a displacement relative to the address of the instruction (PC holds next instructions to be executed).
                    - Relative addressing exploits the concept of locality.
                    - If most memory references are relatively near the instruction being executed, then the use of relative addressing saves address bits in the instruction.
                        
                        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%205.png)
                        
                - Base-register addressing.
                    - For base-register addressing, the interpretation is the following: The referenced register contains a main memory address, and the address field contains a displacement (usually an unsigned integer representation) from that address.
                    - The register reference may be explicit or implicit.
                        
                        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%206.png)
                        
                - Indexing.
                    - This method is the opposite of the previous one.
                    - The address field A holds the base address, and the register holds the displacement. You effective address is the addition of both.
                    - This might be used for iterative operations like array accessing or incrementing/decrementing.
                        
                        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%207.png)
                        
        - Stack.
            - Operand is implicitly on the top of stack.
            - Whenever you want to execute an operation, you can pop top items from the stack (operands) and apply the operation you want.
                
                ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%208.png)
                
- Instruction Format.
    - By saying format we mean the layout of the instruction, which is the opcode and zero or more operands whether explicit or implicit.
    - Implicit operands means that we’re executing our operation (that is defined by opcode) on data that exist in a register and the result is stored in that register, so we don’t mention the operand explicitly.
    - Addressing modes might be explicit or implicit. Explicit addressing mode exist by adding mode field in our instruction whereas implicit addressing modes are implemented by dividing opcodes into groups and each group is associated with a specific addressing mode.
    - Two main issues controlling instruction format are:
        - Instruction length.
            
            ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%209.png)
            
        - Allocation of Bits.
            
            ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2010.png)
            
    - Factors controlling the use of addressing bits.
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2011.png)
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2012.png)
        
    - PDP-8 Microprocessor.
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2013.png)
        
        - In this microprocessor, instruction format changes when opcode changes.
        - It support 3-bit opcode hence we have total 8 operations that can be implemented. We also have 3 types of instructions.
        - Opcode from 0 to 5 has a specific instruction type which is referencing a single address in the memory. The instruction also contains a page bit and indirect bit.
        - Page bit defines whether we’re on page zero or current page.
        - Indirect bit is used to switch between direct or indirect addressing modes.
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2014.png)
        
        - The opcode 6 is associated with I/O instructions, so we have 6 bits in our instruction to address one of 64 devices, and 3 bits to determine I/O command.
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2015.png)
        
        - Opcode 7 is concerned with register reference instructions.
        - Inside each instruction we have three groups of microinstructions that occupy four bits.
        - Each microinstruction has its own instruction format.
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2016.png)
        
        - Notice that group 2 and 3 have the same microinstruction but what distinguishes the latter is bits number 6, 8, 9, 19, and 11 all have constant values and cannot be reset.
    - Variable-Length Instruction
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2017.png)
        
    - PDP-11 Microprocessor.
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2018.png)
        
        ![Untitled](CH11%20-%20Addressing%20Modes%20And%20instruction%20format%20318be8c5eda447e98bc0357cdc847853/Untitled%2019.png)