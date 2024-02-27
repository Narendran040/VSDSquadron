# Riscv-VSD mini reaserch intership

## This repositiry is intended to document the learning outcomes and experience of a 4-week workshop on RISC-V using Open source tools like yosys and Skywater 130nm PDK.

### TASK 0

<details>
 <summary> Summary </summary>
	
Installed all required tools.
</details>	
	<details>
    <summary> Riscv GNU Toolchain</summary>

  ```bash 
    git clone https://github.com/riscv/riscv-gnu-toolchain
    sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool   
    patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev
    ./configure --prefix=/opt/riscv
    make
  ```
    
 ![screen 1](https://github.com/Narendran040/RISCV/assets/157210399/db9eaf8a-81f8-4223-ab89-273b0b598f02)

  ![Screenshot 2024-02-21 181550](https://github.com/Narendran040/RISCV/assets/157210399/8d5b6f8a-650a-41aa-b3e3-696b1f2068f0)
  </details>
 <details>
 <summary> Yosys </summary>
   
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```
![Screenshot 2024-02-21 182022](https://github.com/Narendran040/RISCV/assets/157210399/ab73fc91-e123-47ea-baf3-5705efcfed98)


</details>
<details>
<summary> Iverilog </summary>
  
  ```bash
sudo apt-get install iverilog
 ```
![Screenshot 2024-02-21 182736](https://github.com/Narendran040/RISCV/assets/157210399/d147a3f7-43a1-4832-9e76-e045e4d289ef)

</details>
<details>
 <summary> gtkwave </summary>
  
  ```bash
sudo apt-get install gtkwave
 ```
![Screenshot 2024-02-21 183202](https://github.com/Narendran040/RISCV/assets/157210399/8b052bb8-a3e5-4a2a-bd7a-be6c6cde457e)
</details>
<details>
 <summary> OpenSTA </summary>

 ```bash
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
![Screenshot 2024-02-21 185458](https://github.com/Narendran040/RISCV/assets/157210399/067a5790-087d-4a22-8e1f-ade07bca4b74)
</details>
<details>
  <summary> Ngspice </summary>

 ```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```

</details>
<details>
<summary> Magic </summary>
  
  ```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
 ```

</details>
<details>
<summary> OpenLane </summary>
  
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot
```

</details>
<details>
  <summary> PDKs </summary>

```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

</details>

### TASK 1
	
 <details>
 <summary> Instructions </summary>
Instructions in an Instruction Set Architecture (ISA) represent the fundamental operations that a processor can execute. They are encoded binary patterns understood by the CPU, each corresponding to a specific operation or action. ISAs define the repertoire of instructions that a processor supports, including their formats, encodings, semantics, and behavior. Here's a breakdown of instructions in an ISA:

1. **Operation Codes (OpCodes)**:
   - OpCodes are numerical values or bit patterns that represent specific operations or instructions.
   - Each instruction in the ISA is identified by a unique OpCode that tells the CPU what operation to perform.
   - For example, OpCode 0001 might represent an ADD operation, while OpCode 0010 might represent a SUBTRACT operation.

2. **Instruction Formats**:
   - Instructions are organized into different formats, specifying how the operands and OpCode are encoded within the instruction word.
   - Common formats include R-Type (register), I-Type (immediate), J-Type (jump), and various memory access formats.
   - The format of an instruction determines the fields it contains, such as OpCode, source/destination registers, immediate values, and memory addresses.

3. **Operand Specification**:
   - Instructions operate on operands, which can be registers, memory locations, or immediate values embedded within the instruction.
   - Operand fields within the instruction specify the source(s) and destination(s) for the operation.
   - For example, an ADD instruction might specify two source registers and one destination register where the result will be stored.

4. **Addressing Modes**:
   - Addressing modes determine how operands are specified and accessed within memory.
   - Common addressing modes include direct addressing (using explicit memory addresses), indirect addressing (using pointers or references), and register addressing (using registers to hold operands).

5. **Instruction Semantics**:
   - Each instruction has well-defined semantics that describe its behavior and effects on processor state.
   - Semantics include details such as whether an instruction modifies flags, affects the program counter, or triggers exceptions.
   - For example, a LOAD instruction loads data from memory into a register, while a BRANCH instruction changes the flow of control within the program.

6. **Instruction Set Extensions**:
   - Some ISAs support extensions that provide additional instructions beyond the base set.
   - These extensions may include specialized instructions for multimedia processing, cryptography, vector operations, or other application-specific tasks.

<details>
 <summary> Instruction format types </summary>


1. **R-Type Instructions**:
   - **Description**: R-Type instructions are primarily used for arithmetic, logical, and shift operations where the operands are typically registers.
   - **Format**: In R-Type instructions, the operation code (opcode) is accompanied by register specifiers for source operands and the destination register where the result is stored.
   - **Examples**:
     - ADD: Adds the contents of two registers and stores the result in another register.
     - SUB: Subtracts the contents of one register from another and stores the result in another register.
     - AND: Performs a bitwise AND operation between two registers and stores the result in another register.
     - OR: Performs a bitwise OR operation between two registers and stores the result in another register.
     - SLT (Set on Less Than): Compares two registers and sets a target register to 1 if the first register is less than the second; otherwise, it sets it to 0.

2. **I-Type Instructions**:
   - **Description**: I-Type instructions are typically used for data transfer, immediate operations, and branch operations where one operand is an immediate value (constant) or a memory address.
   - **Format**: In I-Type instructions, the opcode is accompanied by register specifiers and immediate values.
   - **Examples**:
     - ADDI: Adds a register and an immediate value, storing the result in another register.
     - LW (Load Word): Loads a word from memory into a register.
     - SW (Store Word): Stores a word from a register into memory.
     - BEQ (Branch if Equal): Branches to a target address if two registers are equal.
     - LUI (Load Upper Immediate): Loads an immediate value into the upper 16 bits of a register.

3. **J-Type Instructions**:
   - **Description**: J-Type instructions are primarily used for control transfer operations, such as unconditional jumps or branches to specific memory addresses.
   - **Format**: J-Type instructions typically specify target addresses directly or through relative offsets.
   - **Examples**:
     - J (Jump): Unconditionally jumps to a target memory address.
     - JAL (Jump and Link): Jumps to a target address and stores the return address in a register.
     - JR (Jump Register): Unconditionally jumps to the address contained in a register.
     - JALR (Jump and Link Register): Jumps to the address contained in a register and stores the return address in another register.

<details>
 <summary> Example </summary>
 
