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
riscv64-unknown-elg-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```


![intern 1](https://github.com/Narendran040/VSDSquadron-Mini-project/assets/157210399/617e183d-0290-4b71-bf68-1ffee6af8a0b)



### TASK 1
	
 
