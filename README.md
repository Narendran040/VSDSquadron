# Riscv-VSD mini reaserch intership

### TASK 0
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


### TASK 1

 ###  RISC-V base instruction formats

 > Assembly instruction machine code format

 ![assem](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/d230a242-6051-419d-a4be-da35c13696f1)

 
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

![I type](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/31f6b28a-ed2a-4e38-99fd-149d8af7222d)

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


