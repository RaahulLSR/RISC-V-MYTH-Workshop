# RISC-V-MYTH-Workshop
## Introduction

## RISC-V Instruction Set Architecture (ISA)
To communicate with the computer and make the it work in the way we want to work we write the instruction through programming languages such as C which is converted and compiled in assembly language program using RISC-V isa which is then converted into machine language and then into binary language which is understandable by the CPU. And additionally in order for the cpu to implement the Risc-V instruction it needs hardware which is modelled and created by the HDLs 

## Software to hardware

![image](https://github.com/user-attachments/assets/e9db8a02-5d25-408f-b46e-1dd359e317f4)

The above picture describes how the application are run on a CPU. The application software or APPS or written in programming languages which are run on OS. The OS is a software layer which take the full control of the hardware and allocate various hardware resource like clock time, storage etc.. to the various apps running on the system. All the codes are first compiled into instruction according to format of the ISA used and outputs an .exe file .The assembler takes the exe file and converts it into binary language which is understood and executable by the compiler. 

## Integer based calculator
The code of the calculator looks like this,
![image](https://github.com/user-attachments/assets/54021339-a0e2-4b15-855b-2afa4e6d165e)
This will be compiled and an assembly code will be given by the compiler like this,
![image](https://github.com/user-attachments/assets/e71980bd-df2d-4c88-b46c-34f771ea12c2)
From which you can see the various instruction used among which,
![image](https://github.com/user-attachments/assets/a2d603d4-480d-4802-bf12-0b49c80a54e3)
The highlighted are called pseudo instruction
![image](https://github.com/user-attachments/assets/91e42861-5c16-4c06-8263-35300f4e5d4c)
The above highligheted are base integer instruction
![image](https://github.com/user-attachments/assets/ab6a4603-cb7a-467a-b878-66e1dc97fda5)
The above pictures shows the instruction for multiplication and division which belong to RV64M
If we consider the calculator for floating point it looks like this,
![image](https://github.com/user-attachments/assets/2d560c85-4cfc-47ad-9ab6-28fc59c53ef5)
Which when converted to assembly will have ,
 ![image](https://github.com/user-attachments/assets/2b829b52-b19a-4c01-9b67-79a0ae528609)

Among which the highlighted are floating and double precision extension which take care floating point operations. And they belong to RV64F and RV64D respectively.
The RV64IMFD will be able to do multiplication and division in floating point numbers also.
![image](https://github.com/user-attachments/assets/2640dbc3-b923-4dbe-82fd-11666f06f355)
The highlighted area shows some keywords which refer to some registers. This is associated through the ABI the Application Binary Interface.
We will also look into the concept of stack pointer and memory allocation.

## LAB - C program
We will write a integer based C program,
![image](https://github.com/user-attachments/assets/5078db89-16ea-4d12-9226-4f4f8acce12d)
We will execute it and see the output.
![image](https://github.com/user-attachments/assets/2f20e9e7-3fda-40f8-9dd0-42a6b53f60eb)
This is done by the standard GCC c-compiler.
Now we will compile it with riscv compiler.
 ![image](https://github.com/user-attachments/assets/08007efb-dddb-45f0-87aa-328cffc8f1ec)

The syntax is
Riscv64-unknown-elf-gcc -o <file_name to be saved>  <file_name_to_be_used>
Others are flags
-o  to generate object code.
-o1 for optimization -o0 for no optimization and -o3 for aggressive and -os for size.
-march – to specify the arcithecture to be compiled for.
-mabi – to specify the abi interface to use.
 ![image](https://github.com/user-attachments/assets/f7778345-714e-4d37-9da1-3e811e67d7fe)

To view the file,
 ![image](https://github.com/user-attachments/assets/8c247558-1769-49d6-a31d-454a4d60adcc)

We are interested in the main section,

![image](https://github.com/user-attachments/assets/4710013d-341f-44e3-9f7b-b487c07560b3)
There is about (101c4 – 10184)/4 + 1 = 17
We will now use -Ofast
 ![image](https://github.com/user-attachments/assets/ed8394c6-02ff-4425-a557-212adc1abd20)


(100d8 – 100b0)/4 + 1 = 14
Which shows that as we increase the optimization level the number of instruction will decrease.
If we want to see the output of running the Risc-v GCC compiled code then we could use the following command,

![image](https://github.com/user-attachments/assets/fbd2f910-0838-468b-b2b9-e41e00b9f4de)
Next we will see how to debug a code,
For this we will be using spike
 
![image](https://github.com/user-attachments/assets/ef6a12ca-3475-4c48-ad54-1936de2f9bb9)

For starting the debug let first run our code till 100b0 which is the start of the main for this,
![image](https://github.com/user-attachments/assets/e4cf2e53-a8f0-44a1-992f-8b68b5fc4da7)
Ok lets read register A2 for this,
![image](https://github.com/user-attachments/assets/f1816522-4378-4e4d-b175-876741a62425)
 
And after this if we just press enter then it will run the next line of code in main,
![image](https://github.com/user-attachments/assets/1a2fbe33-f899-464f-8fcb-5d529e3bbc4e)
![image](https://github.com/user-attachments/assets/bf9a5d07-97ad-49cf-97ff-d3feaec7f6d8)
The above image the action of lui.
![image](https://github.com/user-attachments/assets/3c9c39b8-fb1f-4ff4-8f30-7e406e2055d5)
 
As you can see now we are able to see the chnge in contents of a0
![image](https://github.com/user-attachments/assets/91db8150-8e45-46d9-95ef-9358662e8e4c)
The above image explains the working of addi

## unsigned numbers
Lets look about the representation 64 bit integers both signed and unsigned 
Human are comfortable with decimal while machines can only understand binary.

![image](https://github.com/user-attachments/assets/9bb4813a-2742-4d37-b579-a4e09f7f561b)

Lets see how this conversion takes place.
Lets take the below example,
![image](https://github.com/user-attachments/assets/a477c543-1205-4875-b9fc-dda5a8c339a8)
The entire 64 bit is called double word and 32 bit number is called word.
The leftmost value or least significant bit is called LSB and right most or most significant bit is called  MSB.
And 8 bits together form a byte and 4 bytes form a word. And 2 words form a double word.
The total number numbers representable by binary is given by 2^n where the n is the number of bits used. And the range is (0 to (2^n)-1).

![image](https://github.com/user-attachments/assets/5b72847c-8855-4f56-8a8c-a7ed9a0b1fe3)
In this a 64 bit representation will be able to use 2^64 numbers.
Conversion from binary to decimal is done by the following way,
![image](https://github.com/user-attachments/assets/334d8cf6-b6cb-45cb-a83d-e65fa62f30df)
  
Multiply the bit 2^position and add all the results to get the decimal equivalent.

![image](https://github.com/user-attachments/assets/5ce24ef9-efbc-4c23-b9bf-3873bbd54330)
Then maximum unsigned number that can be represented is all ones.

## Signed numbers
To represent the negative number we use 2s complement.
![image](https://github.com/user-attachments/assets/8c665e82-8c7c-4822-aef6-9b96422c548e)
To get the 2’s complement of a number:
1.	Write the number in binary (positive form).
2.	Invert all the bits (change 0 to 1, and 1 to 0).
3.	Add 1 to the inverted binary.

In the above case if the MSB is 1 then it is negative number and if it is 0 then it is positive number.
To convert a negative binary to decimal we can use the following two ways
Use the exact same method we used for normal binary but except for the last number where we use -2^63 instead of 2^63.
Or simply we can invert and add one.
![image](https://github.com/user-attachments/assets/64d2fb3e-89ad-4539-809b-ef5a8450fd7c)
Now because we have used the last bit for sign the range and the maximum number is reduced to 
2^(n-1) numbers and the range is -2^(n-1) to  2^(n-1)-1

The below code shows the range,
![image](https://github.com/user-attachments/assets/8ff5462c-f51a-48c8-a805-8f4ea029beb9)
![image](https://github.com/user-attachments/assets/a1f21e3b-a1b0-4a58-9a67-0a8d60de8f5a)
Since the lowest unsigned number is 0 all the negative numbers map to 0.
And the below image represents the amount of space each data type occupies on declration
![image](https://github.com/user-attachments/assets/d15fe5ec-5bf4-492b-8077-694905e6ea6f)
## Introduction to ABI- Application binary Interface.

![image](https://github.com/user-attachments/assets/759f6e4e-8fb2-4795-9093-ba809f1031fa)
The user of computer system doesn’t need to know all the detailed information about the computer but all he need is the appearance and functionality of the computer in a similar manner. The application doesn’t needs to know what exactly happens in the hardware there will be various interfaces between the program and the hardware one among them is ABI

![image](https://github.com/user-attachments/assets/6b7fa628-abfc-4e6d-82b8-5ca04dd249d2)
Some parts of ISA is accessible to OS and some are available to the users directly. These care called User ISA and system ISA. There is a particular way in which the application program can directly call the hardware resource and the way it does it called system calls. This interface that allows system call is called ABI and also sometimes called as system call interface.

The application can access the register via register.
 ![image](https://github.com/user-attachments/assets/665362b1-5d35-4a7d-84cb-24ca53b734ba)

In a RISC-V we have 32 registers. And the width is given by the keyword xlen which is defined by the architecture we use 32 for rv32 and 62 for rv64. For this repo we will assume xlen is always equal to 64.

## why 32 register?? 
For any operations to happen we need to load the data into the register. This can be done in two ways,
•	Directly writing into the register.
•	The data can be loaded from the memory.
Risc-V belongs to little-endian memory system in which the LSB is store in the least memory position and MSB stored in the Highest memory location.

![image](https://github.com/user-attachments/assets/0b970d9d-7542-4fac-9bc4-75afe7985af1)

Lets name the array as M it has three double words then the addressing will look something like this,
![image](https://github.com/user-attachments/assets/b33c8c3d-3d2c-4d8d-9681-e43bbbfc1cc7)
## load instruction

![image](https://github.com/user-attachments/assets/b12541bf-d944-4a7c-a169-f752c4072da2)


## The syntax
LD <register_to_load_data> <offset_to_address>(<register _which_contains_the_memeory_address>)
The syntax for binary instruction will lok something like this,

![image](https://github.com/user-attachments/assets/5cf6dad7-b9e5-47d3-943f-3d41b6d092af)
The opcode is the unique 7 bit code to rpresent the function LD.
Rd refers to the destination register.
Funct3 is used in addition to opcode to represent Load instruction.
Rs1 is the source register.
Immediate is the value that represent the immediate offset value.

Similarly the syntax of add command look like this,
 ![image](https://github.com/user-attachments/assets/223acd3b-89f2-49f1-b90e-88836b83553f)

And the binary code will be formed according to this,
![image](https://github.com/user-attachments/assets/a08880d1-75d6-4a82-9882-ed7c828aa196)

Again 
Opcode + funct3 + funct7 will represent add.
Rs2, rs1 represents source register 1 and 2.
And rd is the destination register.

And after add operation we need to store the contents of register into memory this is done in the following way,


![image](https://github.com/user-attachments/assets/7992c429-f93f-4348-be23-b752145476b8)

And the binary representation of this instruction is formed like this,
![image](https://github.com/user-attachments/assets/70be2c67-cce8-4197-957e-49531410631e)

Again the immediate represent the offset rs2 and rs1 data register and source register respectively.
Opcode + funct 3 represents the function store.


And all the above instruction we saw operates on integers both signed and unsigned. These instructions all belong RV64I – Base Integer instruction and they need to atleast operate the base 47 instruction. The instruction are of various categories,
![image](https://github.com/user-attachments/assets/a1b194f2-cfb6-402a-9eae-74ecf0cd10f7)

The r type operate only on register. 
The I type operate on immediate values.
And s type instruction are used to store.
And if you see here,
![image](https://github.com/user-attachments/assets/89430045-d9b2-4048-ba3a-aada67a68496)

All the registers are represented by 5 bits. So we can represent upto 2^5 = 32 integer registers. And hence we have 32 registers in riscv ISA from x0 to x31.

![image](https://github.com/user-attachments/assets/e242f4aa-b9d0-4566-b7ee-23697ddd5cab)
The ABI does systems calls through this particular registers.
![image](https://github.com/user-attachments/assets/d7777119-acee-4f45-9a2a-2037ad7e0173)
The above image tell about the name and the functionality of each register.

![image](https://github.com/user-attachments/assets/088f2f71-d8c0-4571-9817-1f693595fcb2)
As you can see in the above code how the ABI is used in the code.

## Write C program using ASM language.
Algorithm:
![image](https://github.com/user-attachments/assets/be47be64-f7d0-49eb-9684-664b781ed273)
Here a2-7 are function arguments and a0 and a1 are return arguments.
And Zero is x0 register which is hardwired to zero always.
The above algorithm describes a code to provide sum of digits from 1 to 9.
The c code looks similar to this,
 ![image](https://github.com/user-attachments/assets/1bfaee7c-8a62-4d43-9b07-0fc77056a72b)

And the function load is written in assembly language and it look like this,
![image](https://github.com/user-attachments/assets/e300d1c4-29f6-4f9a-9b4b-b5937a439fc2)
## Step 1: `main()` runs

- Variable `count` is set to 9.
- Then `load(0x0, count + 1)` is called.
  - This passes two arguments to the function:
    - `0x0` (just 0 in hexadecimal)
    - `10` (which is `9 + 1`)
  - These arguments are passed in RISC-V calling convention as:
    - `a0 = 0` → This is not used in your current `load` function
    - `a1 = 10` → This is the actual loop limit, copied into `a2` inside the assembly

---

## Step 2: Inside the `load` Assembly Function

The function:

1. Copies the second argument (`a1 = 10`) into `a2`.
2. Initializes:
   - `a1 = 0` → used as a loop counter
   - `a3 = 0` → used as an accumulator to hold the sum
3. The loop does:
   - Add `a1` (counter) to `a3` (sum)
   - Increment `a1` by 1
   - Compare `a1` to `a2` (which is 10), and loop again if `a1 < a2`
4. After the loop:
   - The sum is in `a3`, which is then moved to `a0` (return value)
   - The function returns to `main()`

### Values added:
`a3 = 0 + 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 = 45`

So, the return value = `45`

---

## Step 3: Back in `main()`

- The return value (in `a0`) is received by C in `result`
- Then, `printf()` displays:
Sum of number from 1 to 9 is 45

And the output shows something like this.
![image](https://github.com/user-attachments/assets/1628c912-9e10-4112-b5e8-086118ce9804)
And the combined object code looks like this,

![image](https://github.com/user-attachments/assets/e6af8f5a-d676-4ac7-934d-25e5a6a21b3b)
Now lets run our c program in the risc-v core.

![image](https://github.com/user-attachments/assets/721abf57-7694-47cd-8757-de590c165bce)
For that first we will give the hex file of our c program to the risc-v CPU code.

For this we will use the picorv32 CPU core.
The design file is named as pi	corv32.v
And the testbench is named as testbench.v
The following snippet shows the part fo program of test bench that reads the hex file,
![image](https://github.com/user-attachments/assets/d12f4467-bbe1-4cc9-b1c1-e52b915c9162)

The following are list of commands that needs to be executed for the program to run on the core,
![image](https://github.com/user-attachments/assets/7921cc5b-b732-4667-843c-7097aa17f37c)
Lets now execute the above commands but before that we must change the file mode of our command file, which can be ddone in the following way,
![image](https://github.com/user-attachments/assets/fa3836cb-c879-4f2c-86da-aae71e4c2037)
And for execution we can use the following command :
 
![image](https://github.com/user-attachments/assets/45743380-c3d6-4c03-b8a8-2e3c6458b184)

This also create the hexfile in this process which looks like this,
This also create the hexfile in this process which looks like this,
![image](https://github.com/user-attachments/assets/d0573bad-db3d-4db0-a39e-87c0e4fdfeef)
And the bitstream file will also be generated during this process,
![image](https://github.com/user-attachments/assets/67ccbb04-3de2-447d-89af-26087b5ce9c9)
This is the file that is used to program the processor.
Now we have completed the process of compiling and running a c program in risc v cpu now lets build our own riscv core.

## Digital Logic using TL Verilog
The basic logic gates are summarized below,
![image](https://github.com/user-attachments/assets/77b5767e-2bdd-477b-90ea-7577d5965a3d)
1. AND Gate
Gives output 1 only when both inputs are 1.
Used for conditions that must both be true.
________________________________________
2. OR Gate
Gives output 1 when at least one input is 1.
Used when any condition being true is sufficient.
________________________________________
3. NOT Gate (Inverter)
Reverses the input: 0 becomes 1, 1 becomes 0.
Used for negating signals or logic.
________________________________________
4. NAND Gate
Outputs 0 only when both inputs are 1.
It is the inverse of the AND gate.
________________________________________
5. NOR Gate
Outputs 1 only when both inputs are 0.
It is the inverse of the OR gate.
________________________________________
6. XOR Gate (Exclusive OR)
Gives output 1 when inputs are different.
Commonly used for bit comparison or toggling.
________________________________________
7. XNOR Gate (Exclusive NOR)
Gives output 1 when inputs are the same.
Used in equality detection circuits.

The combination of these circuit are created and used to achieve the functionality required to achieve it. For example below is the circuit for full adder,
![image](https://github.com/user-attachments/assets/f4e06be0-44f1-4d5c-b3d5-0c9e2681b2d3)
We can also concatenate these circuit to achieve even larger operation, for example the above created full adder can be concatenated to perform a muti bit addition operation
![image](https://github.com/user-attachments/assets/3a43112f-33fd-49db-8a7c-14c3668802df)
The below table summarizes the Boolean operator available to us,


![image](https://github.com/user-attachments/assets/7de9e40d-0ead-434e-87b8-5492ada2109b)
The multiplexer, also most commonly called a mux, is a digital signal selector that can be used to select a signal from a pool of available ones based on the value of select lines. It is a combinational circuit internally. There are various versions of it, like 2x1 and 4x1, where the first number indicates the number of inputs, the second number indicates the number of outputs, and the select lines decide which input is passed to the output. The number of select lines is given by log₂(inputs).
The hardware-level mux is equivalent to a chained if 
statement or assign operator in the software stack
![image](https://github.com/user-attachments/assets/99f2757a-f482-49d9-9eb7-b236db306c28)

## Makerchip IDE
Makerchip IDE is a free, web-based platform for designing and simulating digital circuits using TL-Verilog (Transaction-Level Verilog). TL-Verilog is an extension of traditional Verilog that introduces higher levels of abstraction, making it easier to manage complex designs, pipelines, and control logic. Makerchip allows real-time editing, simulation, waveform viewing, and integration with open-source tools like Verilator. It is widely used in open-source hardware communities to prototype and verify RTL designs more efficiently. 

![image](https://github.com/user-attachments/assets/eff1b993-1e38-48dd-b609-b4af1736a770)
The following snippet shows the program and the output of an inverter,
![image](https://github.com/user-attachments/assets/94a0a7db-3bdf-48a9-b656-314bc325aa7c)
Operating on vectors,
![image](https://github.com/user-attachments/assets/9ccc02e2-2032-46d8-ad75-a9a018237d25)
Usually it is not needed to specify the range of vector in the right hand side while it is essential to do it on the left hand side and the right hand side assumes the length specified by the LHS.

Lets implement the following circuit in TL Verilog now,
![image](https://github.com/user-attachments/assets/cc94c964-c01b-4f52-9ef8-23e292c262fa)
Which when builded comes up like this,
![image](https://github.com/user-attachments/assets/316eb494-65af-4950-b0fd-614bdba5f388)
## sequential logic,
Sequential circuits are a fundamental class of digital circuits in which the output not only depends on the current inputs but also on the past history of inputs. This memory characteristic distinguishes them from combinational circuits. Sequential circuits are essential for implementing storage elements, finite state machines, and timing-dependent logic in digital systems. These circuits use clock signals to control the timing of state changes, making them suitable for synchronizing operations in complex digital systems.

One of the most basic and widely used memory elements in sequential circuits is the D flip-flop (Data or Delay flip-flop). A D flip-flop captures the value of the input data (D) at the moment of the rising (or falling) edge of a clock signal and holds that value until the next clock edge. It has two stable states and one input (D), one clock input, and typically two outputs (Q and Q'). The D flip-flop is essential for data storage, synchronization, and edge-triggered event detection in digital design.

The D flip-flop is a fundamental memory element in sequential circuits, used to store one bit of data. It captures the value at its data input (D) on the active edge of the clock (typically rising or falling edge) and holds it at the output (Q) until the next triggering clock edge. To enhance functionality, most practical D flip-flops include asynchronous Set and Reset inputs, which allow direct control of the output regardless of the clock.
Normal Operation:
•	On the active clock edge, the value of D is sampled and passed to Q.
•	Q holds this value until the next clock edge.
•	The D input has no effect outside of the clock edge (in edge-triggered designs).
Set and Reset:
•	Set (S): When activated (logic 1), it forces Q = 1 immediately, regardless of D or Clock.
•	Reset (R or Clear): When activated (logic 1), it forces Q = 0 immediately, regardless of D or Clock.
•	If both Set and Reset are inactive (logic 0), the flip-flop works in normal clocked mode.
•	If both Set and Reset are activated simultaneously, the output becomes invalid or undefined in most designs.
Usually,
![image](https://github.com/user-attachments/assets/85c29b02-8eee-41f8-9076-fc8c3266b475)
## Fibonacci series
For example the following circuit shows the generation of Fibonacci series.
![image](https://github.com/user-attachments/assets/bae2716b-6277-45bd-aff7-24995b7b0008)
In the makerchip ide it comes out like this
![image](https://github.com/user-attachments/assets/08e4b58b-e1e4-4452-8066-caedc24e625e)
## counter
The circuit is,
![image](https://github.com/user-attachments/assets/7bf6bb71-ad81-4717-a30b-ca3a5410325f)
And the implementation looks like this,
![image](https://github.com/user-attachments/assets/691b522c-9780-4782-b00b-99b15edf6305)
The following picture showcases few important thing is makerchip,
![image](https://github.com/user-attachments/assets/11953644-11d1-469a-9f84-a891db55c718)
Firstly  ‘0 means all zeros ‘X means all Don’t cares. The syntax is
<Bit-Width> ‘ <base- ‘H’or ‘D’ or ‘O’ or ‘B’> <value>
And the simulator use only 2 state variables for simulation.
And the synthesizer and simulation tools truncate or extend when widths are mismatched without raising any warnings.
## Sequential Calculator 
![image](https://github.com/user-attachments/assets/643ef368-4eeb-4e4a-ac5e-94e2c418c52a)

And the circuit comes out like this,

![image](https://github.com/user-attachments/assets/06443465-827f-46d7-a9fc-69ee7a390b8d)
## Pipelining
Pipelining is a technique used in computer architecture to improve the performance of a processor by executing multiple instructions simultaneously in different stages of execution. Instead of completing one instruction before starting the next, pipelining divides instruction execution into several stages (such as fetch, decode, execute, memory access, and write-back), allowing different instructions to occupy different stages at the same time. This overlapping of operations increases instruction throughput and makes more efficient use of hardware resources. Pipelining is widely used in modern CPUs and microcontrollers to speed up processing and enhance system performance without significantly increasing clock speed.
![image](https://github.com/user-attachments/assets/056db727-35aa-49a7-8a68-c973a4190a27)
The above image describes an example of pipelining. It explains the process of calculating the hypotenuse of a right-angle triangle using the Pythagoras theorem. The process involves squaring the inputs, adding them, and taking the square root of the answer. Instead of doing the entire process step by step for each input separately, it takes 3 clock cycles to complete the operation for every input.

So instead of that, the different stages of the operation are isolated. When the first input reaches the second stage, the first stage is fed with the next input. As the input propagates to the next stage, the previous stage will be fed with the next input. In this way, though the first output takes 3 cycles, the subsequent outputs will come in consecutive cycles, hence increasing the efficiency of the processing.
## Advantages of TL Verilog
The below image shows how TL Verilog has simplified the system Verilog in terms code abstraction
![image](https://github.com/user-attachments/assets/2b37041a-55a1-4b20-817a-e82943397cb3)
Code reduction is one of  the most key and interesting features of TL Verilog.
The same circuit can be modelled in different ways for example,

![image](https://github.com/user-attachments/assets/36220414-480d-4e11-b575-66ac4816ad0f)
Though the staging and timing is different but the total outcome remains the same. This process of bucketing the circuit differently and purposefully is called retiming. And this process has been made simple in TL Verilog whereas retiming in system Verilog based design is very bug prone and highly cumbersome.
![image](https://github.com/user-attachments/assets/557f5004-0573-4b8d-ad25-e347d097fdd8)
And one more key advantage of pipelining is that we will be able to clock the circuit to much higher frequency. And having a circuit with faster clock means we will be able to produce more results in a given time.
![image](https://github.com/user-attachments/assets/3eda1f63-6e51-4d29-849a-32a0e121f380)
Without pipeline the circuit something like this,
![image](https://github.com/user-attachments/assets/07ef3299-fcb0-4029-8ae0-1375ad505180)
Adding the pipeline,

![image](https://github.com/user-attachments/assets/4aedeced-d92a-481a-95ca-871ebeb354e7)
## Identifiers and Types in TL Verilog
 ![image](https://github.com/user-attachments/assets/52d8ef6e-aa3f-4d5c-bc8b-694a3fb49833)

Every identifier starts with a $ symbol followed by token and delimitations
The TL Verilog uses strict rules for identifier classification
Lower case and _ for delimitation is used for pipe signal
CamelCase is used for state signals
UPPER_CASE is used for keyword signal.
Numbers cannot be used at the end of the token/identifiers

## Pipelined Fibonacci series


![image](https://github.com/user-attachments/assets/a0ab29f3-04b7-4164-be58-2dd0ca409d48)
The circuit is inherently pipelined circuits.
## Lab pipeline :

![image](https://github.com/user-attachments/assets/8e063d93-e56c-4da2-81fd-3bb00105d3b2)
![image](https://github.com/user-attachments/assets/2f731530-b42c-4a7c-8d02-f2b28c4e6dee)

## Lab counter and calculator : 

![image](https://github.com/user-attachments/assets/177725b7-952f-4e33-937b-c53a82a96f3c)
Solution:
![image](https://github.com/user-attachments/assets/29ad4fa6-9a14-4262-bed0-e405c0df07b6)

## Lab cycle calculator:
![image](https://github.com/user-attachments/assets/5d0fc0ac-9c8b-4e81-91a6-4c69fd92f012)
And the solution is,
![image](https://github.com/user-attachments/assets/941f9ecd-f545-4f3c-96c3-59046ff7d379)
## The concept of validity 
![image](https://github.com/user-attachments/assets/6b973f24-a7f5-482b-8694-08c123e7faf6)
In a pipelined design:
•	Some computations are only meaningful under certain conditions (e.g., only when inputs are valid).
•	We need a way to mark which cycles contain valid data so that:
o	Results are not propagated or used incorrectly.
o	Stages can be gated or flushed accordingly.
the ? symbol.
?my_scope
   $result = $a + $b;
This means:
•	$result is only computed and considered valid when my_scope is valid.


Most of the power consumption of a circuit comes from the clock. And if the global clock is connected to all the flip flps then all the flops will be activated in all the clock edge, which is not needed we can use the clock only when needed. This is achieved by clock gating.
Clock gating is a power-saving technique where the clock signal to parts of a circuit is disabled (gated off) when that part isn't active. This prevents unnecessary switching activity and thus reduces dynamic power consumption.
By gating the clock, we:
Avoid toggling unnecessary flip-flops.
Reduce power, especially in battery-powered or large-scale designs.
![image](https://github.com/user-attachments/assets/b47670f0-c56f-43e0-b9e4-d85151e560d3)
![image](https://github.com/user-attachments/assets/f034059e-dda0-4552-b48b-749603a3dfe4)
The first line :
\m5_TLV_version 1d: tl-x.org
This defines the TL-Verilog version and its source standard. Makerchip uses the m5 toolset from Redwood EDA (formerly TL-X.org).
\SV
   `include "sqrt32.v";
\SV switches from TL-Verilog to SystemVerilog.
sqrt32.v file is a hardware module (function or submodule) to compute the square root.

m4_include_lib(https://raw.githubusercontent.com/stevehoover/makerchip_examples/refs/heads/master/pythagoras_viz.tlv)

Includes an external TL-Verilog file from GitHub, used for visualization and logging (e.g., waveform diagrams or debug info).

m5_makerchip_module
This is a macro that defines the top-level module for Makerchip to simulate or visualize.
\TLV
   // DUT (Design Under Test)
   |calc
\TLV switches back to TL-Verilog syntax.

|calc defines a pipeline stage or a hierarchical logic block named calc.

?$valid
?$valid is a guard condition. The computation is only performed if the signal $valid is asserted (like a handshake signal).

@1
            $aa_sq[7:0] = $aa[3:0] ** 2;
            $bb_sq[7:0] = $bb[3:0] ** 2;

•  @1 is a pipeline stage marker.
•  These lines square the lower 4 bits of inputs $aa and $bb, storing them in $aa_sq and $bb_sq.
The ** operator means exponentiation (in this case, squaring).
@2
            $cc_sq[8:0] = $aa_sq + $bb_sq;
@2 is the next pipeline stage. Here, the Pythagorean sum is computed: c² = a² + b².
@3
            $cc[4:0] = sqrt($cc_sq);
@3 is another pipeline stage. Takes the square root using a predefined function or module (included in sqrt32.v).

m5+pythagorean_viz_and_log(1)
This is a macro call to show visual output (like waveforms or diagrams). It’s used only in Makerchip for educational or debug purposes.


\SV
   Endmodule

Switches back to SystemVerilog and ends the module.

## Distance accumulator :
![image](https://github.com/user-attachments/assets/6bc579e7-6f47-4660-be1d-d32a4b720058)
Solution:
![image](https://github.com/user-attachments/assets/ec723e9a-d1ba-409f-94ac-d6d14ac76da9)
![image](https://github.com/user-attachments/assets/dc45d8f5-f296-4446-b0e5-9b6508634e41)

## cycle calcualtor with validdity
![image](https://github.com/user-attachments/assets/63ef9d8f-585f-4389-986b-8b0d367c0296)
![image](https://github.com/user-attachments/assets/c5892c49-bae3-48d7-8631-1bf3a42d1bb0)
## calcualtor with single value memory
![image](https://github.com/user-attachments/assets/34f14384-397e-49d4-a4e6-662728d4a4d8)
![image](https://github.com/user-attachments/assets/6eb9df1a-de7f-405a-9798-abed1abe596f)
Lexical Reentrance is one of the core and unique features of TL-Verilog (Transaction-Level Verilog) that makes it much more powerful and flexible than traditional HDLs like SystemVerilog or Verilog.
________________________________________
## What is Lexical Reentrance?
Lexical reentrance allows re-entry into a previously declared scope or pipeline stage in the code multiple times. That means you can define some logic inside a stage (e.g., @1), move on to another part of the design, and then later go back and add more logic to the same stage.
This is not allowed in traditional HDLs, where scopes must be strictly nested and closed before moving on.
________________________________________
## Why is this powerful?
In TL-Verilog:
•	You can build a modular, composable, and hierarchical design.
•	You can develop and refine pipeline stages incrementally.
•	Different blocks or modules can collaboratively contribute to the same stage.
•	This leads to cleaner separation of concerns: logic can be written close to the data flow and timing without needing complex rewrites.
Example : 
![image](https://github.com/user-attachments/assets/a6fc268a-29f0-40ce-94bf-38f6ed0f6234)
And in the above example xx[*] means all the bits of xx.
Hierarchy Tutorial
![image](https://github.com/user-attachments/assets/14278531-f86d-49d2-ab7a-5444a5d8cf4e)
## A simple RISC-V architecture,
![image](https://github.com/user-attachments/assets/8934e88a-6996-47be-b978-f543840269f4)
PC – program counter is pointer that points to the next instruction to be executed.
It increments on it own.
This is send to the instruction to the memory, which sends back the instruction to the decode block.
It is going to decode & interpret the instruction. Like parameter of rs,rd,offset etc… it might also interpret a branch instruction with an offset which might move the PC. That’s why decoder also has a control over PC’s increment through the adder.
Most of the instruction are arithmetic instruction. For which we look up into register file. Mostly we need to read two register. These values are fed into the ALU unit. These then perform operation and written back to memory. And most of the time the data will also be stored into the memory. This is done by the Dmem Rd/Wr unit.
Ok lets start building the CPU core,

The implementation plan is as follows,
![image](https://github.com/user-attachments/assets/8045a772-e1c4-4534-b8d6-0db2c760aab8)
The starting point of the design with commented instantiation of Imem and register files and data memory are at,
https://github.com/stevehoover/RISC-V_MYTH_Workshop

the code contains,
* A simple RISC-V assembler.
● An instruction memory containing the sum 1..9 test program.
● Commented code for register file and memory.
● Visualization.
## IMPLEMENTATION OF PC
The first component that we are going to implement is the PC. Which is a standalone component which increases by one unit every cycle the implementation is as follows,
![image](https://github.com/user-attachments/assets/869e6f3e-4d19-4477-b8c2-f2b2e73029ca)
 

## IMPLEMENTATION OF INSTRUCTION MEMORY,

![image](https://github.com/user-attachments/assets/ddcd70ac-1846-4eeb-9376-3659d9c70bc0)
## Connecting instruction memory interfaces:
![image](https://github.com/user-attachments/assets/08f6e2bb-4d38-48f6-a9b1-6433f78c652f)
## Decode:
![image](https://github.com/user-attachments/assets/86eaee65-a4f9-4085-8e45-8ddd1f00e5ea)
![image](https://github.com/user-attachments/assets/066d8b2a-f4ab-4481-bcc0-be2c7f15e937)
![image](https://github.com/user-attachments/assets/8c3b7dfd-d8f2-4ab2-898e-295a04edc998)
![image](https://github.com/user-attachments/assets/94f716f6-23cb-4caf-8eb8-d79d986a2d87)
![image](https://github.com/user-attachments/assets/ffa0475f-bc17-4940-a4cd-4ecf621638f4)
![image](https://github.com/user-attachments/assets/84af6883-9571-4b52-9dd1-e986e5b90f8f)
![image](https://github.com/user-attachments/assets/e2b89d3c-d276-41e0-988c-587db805c746)
![image](https://github.com/user-attachments/assets/3705fdc1-c257-4f19-a838-fa5a68ae0fac)
![image](https://github.com/user-attachments/assets/53c87872-743d-42c5-8264-889dc71d0d9e)
![image](https://github.com/user-attachments/assets/b8f5fa78-b702-4cf9-babf-154bcb59a40e)
![image](https://github.com/user-attachments/assets/c88021fd-68c0-4be8-8fc0-7c13d3abed55)
## Register file read
![image](https://github.com/user-attachments/assets/2f73d47e-d7cf-4729-baca-0bee0e785bc1)
![image](https://github.com/user-attachments/assets/dcc1e3ae-ca61-4210-a0f2-c03de4c87054)

![image](https://github.com/user-attachments/assets/9805f64c-a6db-41ec-bae2-1e07fe987b61)
![image](https://github.com/user-attachments/assets/95d49d9b-a19f-4893-8375-3d5258e2f0e3)
## ALU
![image](https://github.com/user-attachments/assets/e8bc0a06-02ef-4d44-a4e6-6d859231dbd6)
![image](https://github.com/user-attachments/assets/9b95c7dd-79d1-4257-90ee-6396d90176e3)

## Register file Write
![image](https://github.com/user-attachments/assets/1fbb3a11-d9a4-46e3-92b0-5aa5ed554450)
![image](https://github.com/user-attachments/assets/efcb30cb-6ecc-467d-b62c-519adbdedb10)
![image](https://github.com/user-attachments/assets/947ffa63-5755-4480-86ba-32b06aa9231b)

## Branches
![image](https://github.com/user-attachments/assets/93b65770-f162-40c5-913b-bb68bbfc1de8)
![image](https://github.com/user-attachments/assets/749ee73b-15a8-4846-adcf-c0152e6a151d)
![image](https://github.com/user-attachments/assets/b1fcbe8f-bebf-4e18-b80e-05db2e0551d3)
![image](https://github.com/user-attachments/assets/89b9a956-04e4-4485-8802-fb5caa6f31ae)

## Testbench
![image](https://github.com/user-attachments/assets/71490bd9-8f24-45e6-b898-1a1ce584aa99)
## Final implemented cpu

![image](https://github.com/user-attachments/assets/a1ec7c3f-306f-474e-99c8-745afc57c7ba)
The log shows passed
![image](https://github.com/user-attachments/assets/40078a03-2fb9-4082-84bb-57acf6aa66c2)
## ARRAYS;
![image](https://github.com/user-attachments/assets/c414ab34-ac12-4acb-a394-7f4e891818c8)
The working of arrays at the hardware level is described by the above image. Each layer will have a mux to select the value. The number of the layer matches with that particular mux then it read/write the corresponding index value and returns.


## Pipelining the cpu
![image](https://github.com/user-attachments/assets/74a80774-0409-48d2-8792-c69023c15620)
Pipelining is a technique used in digital circuits, especially in processors, to improve instruction throughput (i.e., the number of instructions completed per unit time).

It breaks down the execution of an instruction into several stages, and each stage performs a part of the instruction. While one instruction is in one stage, the next instruction can enter the previous stage, allowing multiple instructions to be in different stages simultaneously. This help in increasing the clock frequency and hence the overall speed of the system.

## Water fall logic
![image](https://github.com/user-attachments/assets/aff029ae-a47b-423f-8d52-b5de4f6e4183)
The above image describes the concept of water fall logic. Though there is just one PC and other hardware module are also just one. But this diagram describes how the hardware block sees itself. And how the values propagate across different pipeline like how water falls across different pipes.

## Hazards
![image](https://github.com/user-attachments/assets/31dfa5af-2984-4c9f-b6e3-4e212e7dfb48)
But wait what if the next instruction is depended on current instruction output that is where problem arises. This is called,Hazards
For example,
![image](https://github.com/user-attachments/assets/77494cdd-9808-4bbd-addf-e7e7d221ee09)
If this happens then we need to discard or wait for few clock cycles like,

![image](https://github.com/user-attachments/assets/0ad5950b-1268-40b5-bbd7-67e210b8c256)
But then the whole purpose and the effort we put to pipeline the cpu goes in vain. So lets us sort out first and simple solution is…

## Cycle $valid
![image](https://github.com/user-attachments/assets/164dce5e-4e0a-4f2d-8110-bef0b5c3fc70)
![image](https://github.com/user-attachments/assets/bbf6679b-94bd-455d-a7b0-1dbd6dddf185)
![image](https://github.com/user-attachments/assets/63bf7568-f546-42df-be8e-eca9a04f56ba)
![image](https://github.com/user-attachments/assets/011ae25b-fdf0-4896-bc34-d1de8cb629d9)

## Register Bypass

![image](https://github.com/user-attachments/assets/271e80d9-8ca9-4a1c-abfd-2cb81bfbac59)

![image](https://github.com/user-attachments/assets/e9111f2b-c0c1-4c17-aeff-70ec071ab8f0)

![image](https://github.com/user-attachments/assets/8d9663b8-17dd-4cdf-9d52-d35940ca392e)
Establishes a bypass (or forwarding) path from the ALU output of the previous instruction directly to the input of the current instruction.

Enables the immediate use of computation results without needing to wait for them to be written to and read back from the register file.
Utilizes a multiplexer to select between the forwarded value and the value from the register file.



## Branches  Hazard

![image](https://github.com/user-attachments/assets/b08da75d-b28f-4b8c-b0d1-cf144faad88e)

![image](https://github.com/user-attachments/assets/135068ed-f0aa-4405-900a-cf25d5006d4c)

![image](https://github.com/user-attachments/assets/828cc3a2-c835-4a18-b49a-7f3bd421daaa)
•	When a branch is taken, the CPU must correctly redirect the program counter (PC) and invalidate any instructions that were speculatively fetched.
•	Due to the three-cycle delay required to decode the instruction, read the operands, and compute the target address, a two-cycle branch penalty is unavoidable.
•	The PC redirection path inherently forms a three-cycle loop.
•	The valid signal logic is modified to ensure that instructions are marked valid only if previous branches are not taken.
•	For normal sequential execution, the PC update follows a one-cycle loop, while for branch redirection, the three-cycle loop remains.
•	Simulate the design using a model that closely achieves one instruction per cycle.
•	Confirm the correctness of the bypass and branch-handling mechanisms through validation.

## Completing the CPU

![image](https://github.com/user-attachments/assets/77eb3cb7-5cc1-4052-a38a-2fcb60612f03)

![image](https://github.com/user-attachments/assets/1f230fa6-dca7-446a-9c4e-69efab9f89cd)

![image](https://github.com/user-attachments/assets/a2cb862e-6a20-4b94-ab57-c80f6fa1f7fe)

![image](https://github.com/user-attachments/assets/732869da-546c-4af3-a144-7eeacf82b365)
## Load hazards

![image](https://github.com/user-attachments/assets/60e209d8-903d-41ec-b4fc-01647fd5a0f9)
Solution 

![image](https://github.com/user-attachments/assets/3c422597-1330-4d42-83bb-d37a79541a6a)

![image](https://github.com/user-attachments/assets/6d02d718-20e8-43a2-a6fa-0e34a2f1313f)

![image](https://github.com/user-attachments/assets/21b9bb85-798b-4bd5-a808-d5764bd7fc37)

![image](https://github.com/user-attachments/assets/8552904d-8314-4294-a4eb-9a98fa2a54a5)
![image](https://github.com/user-attachments/assets/19fdbb74-901d-440e-8339-d1e53b9715e1)

## Jumps

![image](https://github.com/user-attachments/assets/f4ad3b12-b53d-412b-abe3-03619b9bb4ae)

![image](https://github.com/user-attachments/assets/528a2566-a3ac-4f52-916f-919b834d8cec)

## final implemted design

![image](https://github.com/user-attachments/assets/25267e32-4e3f-4736-a875-a5c5e9c480cf)


![image](https://github.com/user-attachments/assets/c97dda25-fe3a-486a-b09f-c7efa048a0af)


![image](https://github.com/user-attachments/assets/27472945-7a11-45b9-a105-54961d0b0994)


![image](https://github.com/user-attachments/assets/7f331f13-cdae-43aa-a9b0-ebf0f727bdd7)


## conclusion

## References




























