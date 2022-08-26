# CH10 - Instruction Set.

- Introduction.
    - Instruction set is some instructions that are defined by the computer architecture, so that you can do a predefined operations on your data by activating or disactivating some parts of your computer hardware for the sake of data processing.
    - Machine instruction characteristics - Overview.
        1. **Elements of machine instruction** : We need to define the construction of an instruction and its fields that represents the instruction.
        2. **Instruction Representation** : Should we use binary to represent an instruction? This must be inconvenient so we might use hexadecimal. We still might need a way to interpret the program we write into a machine level code.
        3. **Instruction types** : Our instruction might be a data processing instruction, data storage instruction, or other types that we need to define.
        4. **Number of addresses** : Define the number of addresses needed to store the data we want to work on and the result of that data, as well as other types of addresses that will be discussed.
- Machine Instruction Characteristics.
    - Elements of Machine Instruction.
        
        ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled.png)
        
        - We’re going to revisit instruction cycle once again.
        - We first get the address of the instruction, we read that address then fetch that instruction by its address. After that, we decode the instruction operation (op-code which is a field in our instruction we fetched) to know what should we do with the data (operands).
        - The instruction we fetched has a field for the operands that we’ll be working with, so we extract the address of the operand and we then fetch that operands. The instruction may also have addresses for two operands.
        - After we fetch the two operands, we start do the data operation and we store the result at another address.
        - The cycle then continues by fetching the next instruction.
        - You can deduce that we need about four fields in our instruction which are :
            - Op-code.
            - First and second operands (two fields).
            - Result address.
            - Next instruction address.
        - The source operands and results operands might be read from or written to the main or virtual memory, CPU registers, or IO devices.
        
        ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%201.png)
        
    - Instruction Representation.
        - Each instruction is represented as set of binary digits that are divided into fields.
        - The first field is the opcode which is basically defines the operation code that is thereafter translated into a symbolic representation like ADD, SUB, LOAD, or any other operation.
        - The instruction may also have other fields for operands which we’d apply our operation with and an address to store the result of that operation.
        - You basically have a table that maps each opcode to its equivalent operation. For example, the ADD operation may have opcode 101. Basically you don’t have to memorize the opcode, you can just use the operation’s name and that would be mapped to its equivalent binary value.
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%202.png)
            
    - Instruction Types.
        - This is divided into groups :
            - Data Processing : Arithmetic and Logic instructions (ADD, SUB,, AND, OR, etc.).
            - Data Storage : Memory instructions to read to or write from memory (LOAD operation for example).
            - Data Movement : I/O Instructions to write data to peripheral devices.
            - Control : Test and Branching instructions which are used to run code based on conditions (if, while, etc.).
    - Number of Addresses.
        - We previously said that the instruction format is divided into opcode, first operand, second operand, and next instruction’s address.
        - Say you have a 1 MB memory which needs 20 bits to address a word in that memory.
        - So you need 20 bits to address the first operand, another 20 bits to address the second operand, another 20 bits to store the result, and another 20 bits to address the next instruction. This means that you need 80 bits + opcode bits (say 10 bits so you have 90 in total) to format an instruction.
        - Four Addresses
            - The previous instruction is consisted of **four-addresses**, the first operand, second operand, result, and next instruction address. Notice that next instruction field is a useless field because the program counter holds the current instruction and can easily add 1 or the number of bits occupied to the current instruction to get the next instruction so it’s **extremely rare** to use.
                
                ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%203.png)
                
        - Three Addresses
            - The next type is the **three addresses** in which you remove the next instruction field, so you now have only the first and the second operands as well as the result of the operation. So say you have two operands B and C, and you apply an operation OP (ADD, SUB, or any operation), and you now store the result inside address A. This type is better than the previous one, but you can reduce the size once more.
                
                ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%204.png)
                
        - Two Addresses
            - In two addresses type, you can let one of the operands serve as an operand and result. This might require some extra work as you need to hold some results temporarily.
                
                ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%205.png)
                
        - One Addresses
            - The penultimate type is the one-address type. In that type, you have an implicit second address. So you put the operand A to the **accumulator** (a register in which intermediate arithmetic logic unit results are stored) in which your data resides (second operand), and you can apply the operation on the operand and the data, and the result is fed into the accumulator again.
                
                ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%206.png)
                
        - Zero Addresses
            - The last type is zero-address in which all addresses are implicit. In this type, you use a stack and you keep pushing data (operands) to the stack such that once you see the operation, you pop the result from the stack.
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%207.png)
            
        - Example on Addresses.
            
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%208.png)
            
            - You might notice in the previous example, the more addresses you have, the less number of instructions you need to execute. However, the addresses with less instructions have complex ones which might require more registers.
            - More instructions (in case of one-address instructions) means faster fetch/execution of instructions
            - Check problem 10.6 at Stallings book to see a similar problem.
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%209.png)
            
            - How should we decide the correct number of addresses to use ? The answer is “it depends”. You should construct the format of an instruction such that the bandwidth of your system bus can fetch/execute that instruction in a single cycle, actually you want to execute your instruction with the least amount possible of cycles. So in our first example of instruction with 130 bits, you need a bus that can transmit 130 bits per cycle, which would result in high cost.
            - So your design decision of instruction format should be aligned with the bandwidth of the bus.
- Fundamental Issues of Instruction Set Design.
    - First things first, we need to define how many opcodes we have, what is the task of each one, and how complex are they.
    - We also have to define the data types for the operands.
    - We need to define the instruction format. You should define the length of opcode field as well as the fields for addresses.
    - We need to know the number of CPU registers available, and which operation can be performed on which registers.
    - Last thing we need to consider is the addressing mode. Recall the instruction cycle, an address calculation is performed to fetch the instruction. It’s not straightforward to just get the correct address of the instruction from the memory, a translation for the address should be performed. Addressing mode is the translation that happens for the instruction address so that it can be fetched correctly from the memory.
    
    ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2010.png)
    
    ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2011.png)
    
- Type of Operands.
    - **Addresses** : You can do operations on addresses. Addressing modes helps on determining how to read these addresses.
    - **Numbers** : Integer/Floating point, you should also consider rounding and overflow.
    - **Characters** : Like ASCII code (8 bits).
    - **Logical Data** : Data that we read it bit by bit (for
        
        ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2012.png)
        
- Type of Operations.
    - Data Transfer.
        - All instructions in machine language have data movement, your data may be read from or written to IO devices or memory.
        - So the location of source and destination operands should be specified. The location might be :
            - Memory.
            - Register.
            - Top of stack.
        - The length of transferred data should be also specified as well as the addressing modes.
        
        ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2013.png)
        
    - Arithmetic.
        - We have two types of operators, binary and unary.
        - Binary means two operands and unary means single operand.
        - We can add, subtract, multiply, or divide two operands.
        - Single-operand instructions includes absolute, negative, increment or decrement.
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2014.png)
            
    - Logic.
        - Bitwise operations : AND, OR, XOR, NOT, etc.
        - Notice that AND operator might be used to do masking (extracting a tag or line field in cache line for example) and XOR is used to get ones-complement.
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2015.png)
            
        
        - We have three different types of shifting :
            - Logic shift
            - Arithmetic
            - Rotating
        
        - Logic Shift
            - In this type you insert a kill value (zero) to the digits that are gone. For example if you right shift this binary number by one bit 10101 you would get 01010.
                
                ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2016.png)
                
        - Arithmetic shift.
            - In this type, the sign bit (most significant bit) is preserved while shifting.
                
                ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2017.png)
                
        - Rotate shift.
            - In rotation, you don’t add any zeros. The digit that was dismissed on one side, is added to the other side (like circular-buffer or in a round-robin manner).
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2018.png)
            
    - Conversion.
        - Some operations are associated with converting from binary to decimal and vice versa.
    - Input/Output.
        - This kind of operations may be done using data movement instructions (memory mapping) or by a separate controller (DMA).
        - **DMA** stands for **direct memory access**. Say you have an image to be transferred from the hard disk and displayed on a screen. You don’t need to interrupt the CPU for that as no processing on that image is actually needed. So rather than interrupting the CPU, you can directly fetch the image from the hard disk, then transfer it to the main memory and start displaying it on the screen.
        
    - System Control.
        - Set of operations that can only be used by people who are programming the OS.
        - These operations can only run on certain mode (Kernel mode) and have privileged instructions.
    - Transfer of Control.
        - It’s basically the branching instructions, like unconditional and conditional branching.
        - If and while statements are examples of conditional branching where as goto is an example of unconditional branching.
        - Looping can be implemented with branching. Basically a condition is checked so to make sure if the loop continues or not. So in the right example, you keep executing from address 301 to 309, in 309 you check if the register R1 equals zero (**ISZ = instruction skip if zero**), if it’s true then jump to 311 and ignore 310, otherwise go to 310 which would bring you back to 301 (the start of the loop).
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2019.png)
            
        - Another important example of transfer of control is procedure call instructions. You might have two functions, the first function calls the second one. Once the second one is returned, you need to get back the first function to continue its execution. You have to find a way to store the address of the line that called the second function so to have the ability of continuing the execution.
        - The first option is using a register that stores that address and is checked once we return from the second function.
        - A second option is to pass that address to the second function, and whenever we return from that function, we have check that register to get back to the correct line.
        - A third option can also used by using a stack, once you return from the function, you can pop that call from the stack.
            
            ![Untitled](CH10%20-%20Instruction%20Set%20543af75afb5e4ceb8bc60a6cd713d34e/Untitled%2020.png)
            
    
- Readings
    - If you have extra time, kindly read Linda’s chapter 5.