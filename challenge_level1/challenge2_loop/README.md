![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Priyanshu-1012/assets/39450902/796f3662-185f-4a85-bc21-ab45fa5f7a42)
the bug causing an infinite loop is in the loop label inside the RVTEST_CODE_BEGIN section of the test.s file. 
The problem lies in the logic of the loop and how the test cases are being loaded and checked. The loop is supposed to 
iterate through the test_cases array, but the loop does not have a proper termination condition. It keeps looping indefinitely
(repeated execution of the same test case).

#### bug fix
To fix the infinite loop, i introduced an exit condition to the loop by adding a loop counter. The loop counter (register t5) was initialized with the number of test cases. With each iteration of the loop, the counter was decremented, and the loop continued until the counter reached zero. This way, the loop was properly terminated after testing all the cases. 

```assembly
test_pass:
  addi t5, t5, -1  # Decrement the loop counter
  bnez t5, loop    # Branch to loop if the counter is not zero
```

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Priyanshu-1012/assets/39450902/e7b7c4f7-ceb1-435b-b2a3-57e1556043d4)


## Revised code

```assembly
# See https://gitlab.com/vyoma_systems/common/-/blob/main/LICENSE.vyoma for more details
 
#include "riscv_test.h"
#include "test_macros.h"

RVTEST_RV32M
RVTEST_CODE_BEGIN

  .align 2
  .option norvc
  li TESTNUM, 2

  la t0, test_cases
  li t5, 3

loop:
  lw t1, (t0)   
  lw t2, 4(t0)  
  lw t3, 8(t0)
  add t4, t1, t2

  beq t3, t4, test_pass  # check if sum is correct
  j fail

test_pass:
  addi t5, t5, -1  # Decrement the loop counter
  bnez t5, loop    # Branch to loop if the counter is not zero

test_end:

TEST_PASSFAIL

RVTEST_CODE_END

.data
RVTEST_DATA_BEGIN

test_cases:
  .word 0x20      # input 1
  .word 0x20      # input 2
  .word 0x40      # sum
  .word 0x03034078
  .word 0x5d70344d
  .word 0x607374C5
  .word 0xcafe
  .word 0x1
  .word 0xcaff

RVTEST_DATA_END
```
