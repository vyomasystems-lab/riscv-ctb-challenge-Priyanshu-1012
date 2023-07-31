![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Priyanshu-1012/assets/39450902/b3b6a392-1b1f-4793-9eb3-9295223e3025)

#### 2 errors...

1. In the first case, the instruction ```and s7, ra, z4``` is not valid because 'and' requires two source registers, but the third operand 'z4' is not a valid register. It seems like 'z4' is a typo or an undefined register, which is causing the error.
2. In the second case, the instruction andi s5, t1, s0 is not valid because 'andi' is used for bitwise AND with an immediate value, but 's0' is not a valid immediate value; it's a register.

#### Fixes....
1. Replace ```and s7, ra, z4``` with ```and s7, ra, ra```
2. Replace ```andi s5, t1, s0``` with ```and s5, t1, s0```

#### Run after removing the bugs

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Priyanshu-1012/assets/39450902/cd02f3fa-f786-4d7b-ad4c-7bbaf9ad6c98)
