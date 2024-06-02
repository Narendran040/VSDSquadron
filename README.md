# Riscv-VSD mini reaserch intership

### TASK 1
 ### Compiling C code using Risc-V GNU Toolchain

> C program

 ```
#include<stdio.h>
int main() {
  int sum=0, i=1, n=100;
  for(i = 1; i <= n; ++i){
    sum += 1;
  }
  printf("Sum of numbers from 1 to %d is %d \n",n,sum);
  return 0;
}
```

> Compiling C program

```
gcc sum1ton.c
./a.out
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```


![intern 1](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/617e183d-0290-4b71-bf68-1ffee6af8a0b)


![intern 2](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/8e1a58d4-4771-49ab-b1ff-b8bc12412c2a)

![intern3](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/42773ea0-7e34-4700-b575-fac16604f2f5)


![intern4](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/899b8878-4c5d-4841-b724-7b17d972fe50)

> Ofast

```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

![intern5](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/7d82cb8f-f987-4ac9-b806-0ebb03a56863)


![intern6](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/202a709b-5cd8-4103-ace6-41a0b5e0f496)


### TASK 2

 ###  RISC-V base instruction formats

 > Assembly instruction machine code format

![32 bit](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/5c1716d9-ef5c-4107-b0b4-d6f3b766a8c4)


 
 . opcode (operation code), rd(destination register),rs1 & rs2 ( source registers),func3( 3-bit field that specifies the operation (function) within a particular opcode.),imm(immediate).




> R-type

![rtype](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/f5ae111f-695b-499d-b0e0-a014f882af2b)


The R-type command format is very clear. In the actual encoding process, the arrangement of encoding positions is meaningful. For example, the encoding position of the three register indexes in different instruction formats are always the same. Index of Rd is at 11-7, Index of rs1 is at 19-15, and Index of rs2 is at 24-20. This is their fixed position. Some instructions may not be useful. The index to the partial register. For example, there is no rs2 in the second instruction type I-type, but there are rs1 and rd and their indexes are in the corresponding positions. For another example, in s-type funct3 is at bits 14-12. The opcode is available in all instruction formats, and the position remains unchanged, always bit 0-6.


The 32-bit R-type instruction format consists of the following fields:

opcode: 7 bits - Specifies the operation to be performed.
rd: 5 bits - Destination register.
funct3: 3 bits - Further specifies the operation (used with the opcode).
rs1: 5 bits - Source register 1.
rs2: 5 bits - Source register 2.
funct7: 7 bits - Further specifies the operation (used with the opcode and funct3). 

> I type

![i](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/2cf2c7c4-47f2-404a-b3de-cbd782ba47e2)


The I-type (Immediate type) instructions in RISC-V are used for operations that involve an immediate value (a constant embedded in the instruction itself), rather than a second source register. This format is used for various operations including arithmetic operations with immediate, load instructions, and some control instructions.

The 32-bit I-type instruction format consists of the following fields:

imm[11:0]: 12 bits - Immediate value.
rs1: 5 bits - First source register.
funct3: 3 bits - Specifies the operation within the opcode.
rd: 5 bits - Destination register.
opcode: 7 bits - Specifies the operation to be performed.

> S type


![1663416913008](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/96021906-75d2-4b2a-ba30-be814af48696)


The characteristic of S-type instruction is that there is no rd register. In this type of instruction, the immediate is divided into two parts, the first part is in bit11-5, and the second part is in bit4-0. The 5 bits of the immediate 4-0 occupy the position of rd in other instruction formats, and 5-11 occupy the position of funct7. Explain that the command format does not need to write back. That is, read the two values from the two registers and perform the operation together with the immediate, and write the result to the register after the operation is over.

The 32-bit S-type instruction format consists of the following fields:

imm[11:5]: 7 bits - The upper 7 bits of the immediate value.
rs2: 5 bits - The second source register, which contains the data to be stored.
rs1: 5 bits - The first source register, which contains the base address.
funct3: 3 bits - Specifies the operation within the opcode.
imm[4:0]: 5 bits - The lower 5 bits of the immediate value.
opcode: 7 bits - Specifies the operation to be performed.

> U type

![u type](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/b8991df5-4bf5-4235-b26e-65afaa69e398)

 
 A 20-bit immediate is provided in the U-type instruction. The final operation result is related to the 20-bit immediate, and the result is written back to the rd register. The opcode determines the type of operation. There are no funct3, rs1, rs2, and funct7 in U-type. This type of instruction structure is very simple.

 The 32-bit U-type instruction format consists of the following fields:

imm[31:12]: 20 bits - The immediate value, which is placed in the upper 20 bits of the destination register.
rd: 5 bits - The destination register.
opcode: 7 bits - Specifies the operation to be performed.

> B type

![b](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/3ef90b40-cfce-4bdf-af6d-ab40a6e140db)

B-type instructions are mainly used as branch instructions, but they are conditional Branch. It means to decide whether to jump or not need to depend on whether the condition is valid. The B-type machine code structure is shown in Figure 2-1. The instruction does not include rd register and funct7, but contains rs1, rs2, funct3 and immediate. The immediate is divided into two areas. The encoding of B-type instruction immediate is out of order. The reason is not described in detail here. There is a specific article on the official site explaining why it is out of order. In short, it has been verified that the effect on CPU operation function when the immediate number sequence is in this order is very well. But the immediate is disrupted, so it will be decoded when the CPU executes in the future. After decoding, the CPU needs to restore the disrupted immediate in order. For example, when the CPU gets a B-type instruction, the immediate in it is scrambled, and the CPU needs to arrange the immediate in the order of 12-1 to restore the immediate.

The 32-bit B-type instruction format consists of the following fields:

imm[12|10:5]: 7 bits - Part of the immediate value for the branch offset.
rs2: 5 bits - The second source register.
rs1: 5 bits - The first source register.
funct3: 3 bits - Specifies the branch condition.
imm[4:1|11]: 5 bits - Part of the immediate value for the branch offset.
opcode: 7 bits - Specifies the branch operation.

> J type

![j](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/fd94bed8-9138-4d31-a38d-114ca274b59e)

The J-type (Jump type) instructions in RISC-V are used for unconditional jumps to a target address, which is computed by adding a 20-bit immediate value to the current program counter (PC). The primary instruction in this category is JAL (Jump and Link), which stores the return address in a register.

The 32-bit J-type instruction format consists of the following fields:

imm[20|10:1|11|19:12]: 20 bits - The immediate value for the jump offset, split into multiple parts within the instruction.
rd: 5 bits - The destination register for the return address.
opcode: 7 bits - Specifies the jump operation.

> Identifying various Riscv instructions and their 32-bit code 

R-Type Instructions Encoding

.ADD r6, r2, r1: 0000000 00001 00010 000 00110 0110011

.SUB r7, r1, r2: 0100000 00010 00001 000 00111 0110011

.AND r8, r1, r3: 0000000 00011 00001 111 01000 0110011

.OR r9, r2, r5: 0000000 00101 00010 110 01001 0110011

.XOR r10, r1, r4: 0000000 00100 00001 100 01010 0110011

.SLT r11, r2, r4: 0000000 00100 00010 010 01011 0110011

.SRL r16, r14, r2: 0000000 00010 01110 101 10000 0110011

.SLL r15, r1, r2: 0000000 00010 00001 001 01111 0110011

I-Type Instructions Encoding

.ADDI r12, r4, 5: 000000000101 00100 000 01100 0010011

.LW r13, r1, 2: 000000000010 00001 010 01101 0000011

S-Type Instructions Encoding

.SW r3, r1, 2: 0000000 00011 00001 010 00010 0100011

B-Type Instructions Encoding

.BNE r0, r1, 20: 000000 00001 00000 001 01010 1100011

.BEQ r0, r0, 15: 000000 00000 00000 000 01111 1100011

### Task 3

> BLOCK DIAGRAM OF RISC-V RV32I

![Screenshot 2024-06-01 220845](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/5575fafe-f927-4cf7-a104-71cab4b99235)

> INSTRUCTION SET OF RISC-V RV32I

![Screenshot 2024-06-01 222418](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/daec22fa-a615-4c02-a02c-844370bf5164)

Computational Instructions:

ADD rd, rs1, rs2: Add two registers and store the result.

SUB rd, rs1, rs2: Subtract one register from another and store the result.

AND rd, rs1, rs2: Perform a bitwise AND operation between two registers.

OR rd, rs1, rs2: Perform a bitwise OR operation between two registers.

XOR rd, rs1, rs2: Perform a bitwise XOR operation between two registers.

SLL rd, rs1, rs2: Perform a logical left shift operation on a register.

SRL rd, rs1, rs2: Perform a logical right shift operation on a register.

SLT rd, rs1, rs2: Set a register to 1 if one register is less than another.

SLTU rd, rs1, rs2: Set a register to 1 if one register is less than another (unsigned).

Memory Instructions:

LW rd, offset(rs1): Load a word from memory into a register.

SW rs2, offset(rs1): Store a word from a register into memory.

LB rd, offset(rs1): Load a byte from memory into a register, sign-extending it.

SB rs2, offset(rs1): Store a byte from a register into memory.

LUI rd, immediate: Load an immediate value into the upper bits of a register.

Control Flow Instructions:

BEQ rs1, rs2, offset: Branch if two registers are equal.

BNE rs1, rs2, offset: Branch if two registers are not equal.

BLT rs1, rs2, offset: Branch if one register is less than another.

JAL rd, offset: Jump and link (store the return address) to a new address.

JALR rd, rs1, offset: Jump and link (store the return address) to an address specified by a register and an offset.d

> FUNCTIONAL SIMULATION

.Icarus Verilog is an implementation of the Verilog hardware description language.

.GTKWave is a fully featured GTK+ v1. 2 based wave viewer for Unix and Win32 which reads Ver Structural Verilog Compiler generated AET files as well as standard Verilog VCD/EVCD files and allows their viewing.

> Installing iverilog and gtkwave

For Ubuntu

Installation iverilog and GTKWave:

```
sudo apt-get update
sudo apt-get install iverilog gtkwave
```
> Clone this repository for netlist files for simulation:

```
git clone https://github.com/vinayrayapati/rv32i.git
./rv32i
```


> To simulate and run the verilog code

```
iverilog -o rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
./iiitb_rv32i
```

![task 3](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/7eeba585-c5bb-4f6e-ab26-b3429c119c99)


> To see the output waveform in gtkwave

```
gtkwave iiitb_rv32i.vcd
```

![task 3 1](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/5941cb72-55a2-45ac-8fd4-b9d0a7fe39b9)


> The Output Waveform

![task 3 2](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/3a721525-6f58-43d3-85f8-4e9d4cf4ef71)


![task 3 4](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/a7ab9f73-d88a-4c32-a195-7c7cc250a9ca)


> Synthesis

Synthesis transforms the simple RTL design into a gate-level netlist with all the constraints as specified by the designer. In simple language, Synthesis is a process that converts the abstract form of design to a properly implemented chip in terms of logic gates.


> Commands for installing Yosys
```
git clone https://github.com/YosysHQ/yosys.git
make
sudo make install make test
```


> Create a yosys_run.sh file, which is the Yosys script file used to run the synthesis


```
read_liberty -lib lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog iiitb_rv32i.v
synth -top iiitb_rv32i	
dfflibmap -liberty lib/sky130_fd_sc_hd__tt_025C_1v80.lib
proc ; opt
abc -liberty lib/sky130_fd_sc_hd__tt_025C_1v80.lib
clean
flatten
write_verilog -noattr iiitb_rv32i_synth.v
```

> Verilog files folder
```
yosys
script yosys_run.sh
```

Check for .v files by using ls -ltr 

 .Synthesized netlist is written in the "iiitb_rv32i_synth.v" file.

 > GATE LEVEL SIMULATION

 Following are the commands to run the GLS simulation

```
iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 ../verilog_model/primitives.v ../verilog_model/sky130_fd_sc_hd.v iiitb_rv32i_synth.v iiitb_rv32i_tb.v
./a.out
gtkwave iiitb_rv32i.vcd
```
### Task 4

### Full Adder using VSDSquadron Mini

![task 4](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/c242534b-87c5-43a3-a2b3-6d4c541690c1)

> Overview

This project involves the implementation of a Full Adder combinational circuit using VSDSquadron Mini, a RISCV-based SoC development kit. Full Adder is a very important circuit in digital electronics, widely used in creating the design of n-bit Adder circuits. A full adder circuit is a digital circuit that adds two binary digits and a carry-in digit to produce a sum and carry-out digit. It’s a central component of most digital circuits that perform addition or subtraction. This project demonstrates the practical application of digital logic and RISC-V architecture in executing arithmetic operations, reflecting the process of reading and writing binary data through GPIO pins, implementing the operation of full adder through digital logic gates which is simulated using PlatformIO IDE and thus displaying the outputs using LEDs

>Components Required

VSDSquadron Mini

Push Buttons for Input of binary data

2 LEDs for displaying the Output

Breadboard

Jumper Wires

VS Code for Software Development

PlatformIO multi-framework professional IDE

> Hardware Connections

Input: Three inputs of a single bit are connected to the GPIO pins of VSDSquadron Mini via push buttons mounted on the breadboard.

Outputs: Two LEDs are connected to display the result of Full Adder
The GPIO pins are configured according to the Reference Manual, ensuring the correct flow of signals between the components

> Truth Table to Verify the Full Adder

| A | B | Cin | Sum | Cout |
|---|---|-----|-----|------|
| 0 | 0 |  0  |  0  |   0  |
| 0 | 0 |  1  |  1  |   0  |
| 0 | 1 |  0  |  1  |   0  |
| 0 | 1 |  1  |  0  |   1  |
| 1 | 0 |  0  |  1  |   0  |
| 1 | 0 |  1  |  0  |   1  |
| 1 | 1 |  0  |  0  |   1  |
| 1 | 1 |  1  |  1  |   1  |

> Pins used for connection

|    |Name|VSDSquadron Mini|
|----|----|----------------|
Pin|Analog I/O pin|PC4,PD1,PD2,PD3|
|Communication|SPI|PC5(SCK)|
|||GND|

PC4: Input A

PD1: Input B

PD2: Input Cin

PD3: Output Sum

PC5 (SCK): SPI Clock

> SPI Overview

SPI is a synchronous serial communication protocol used for short-distance communication, primarily in embedded systems. It allows multiple devices to communicate with one another by sharing a common clock signal, which ensures data is transmitted in a synchronized manner.


> How to program

```
// Full Adder Implementation

// Included the requried header files
#include<stdio.h>
#include<debug.h>
#include<ch32v00x.h>

// Defining the Logic Gate Function 
int and(int bit1, int bit2)
{
    int out = bit1 & bit2;
    return out;
}
int or(int bit1, int bit2)
{
    int out = bit1 | bit2;
    return out;
}
int xor(int bit1, int bit2)
{
    int out = bit1 ^ bit2;
    return out;
}

// Configuring GPIO Pins
void GPIO_Config(void)
{
    GPIO_InitTypeDef GPIO_InitStructure = {0}; // structure variable used for GPIO configuration
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE); // to enable the clock for port D
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE); // to enable the clock for port C
    
    // Input Pins Configuration
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU; // Defined as Input Type
    GPIO_Init(GPIOD, &GPIO_InitStructure);

    //Output Pins Configuration
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_4 | GPIO_Pin_5;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP; // Defined Output Type
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz; // Defined Speed
    GPIO_Init(GPIOC, &GPIO_InitStructure);
}

// The MAIN function responsible for the execution of program
int main()
{
    uint8_t A, B, Cin, Sum, Carry; // Declared the required variables
    uint8_t p, q, r, s, t; 
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
    SystemCoreClockUpdate();
    Delay_Init();
    GPIO_Config();

    while(1)
    {
        A = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_1);
        B = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_2);
        Cin = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_3);
        s = xor(A, B);
        Sum = xor(Cin, s);
        p = and(A, B);
        q = and(B, Cin);
        r = and(Cin, A);
        t = or(p, q);
        Carry = or(r, t);

        /* SUM */
        if(Sum == 0)
        {
            GPIO_WriteBit(GPIOC, GPIO_Pin_4, SET);
        }
        else
        {
            GPIO_WriteBit(GPIOC, GPIO_Pin_4, RESET);
        }

        /* CARRY */
        if(Carry == 0)
        {
            GPIO_WriteBit(GPIOC, GPIO_Pin_5, SET);
        }
        else
        {
            GPIO_WriteBit(GPIOC, GPIO_Pin_5, RESET);
        }
    }
}
```

