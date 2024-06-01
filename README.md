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
	
 
