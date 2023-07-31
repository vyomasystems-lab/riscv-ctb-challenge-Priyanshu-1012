![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Priyanshu-1012/assets/39450902/412c49f0-4703-486a-841a-ee1b0f63b85c)

## bug
makefile is for rv32i isa and file is rv64m...conflict

makefile fix

```
all: compile disass spike

compile:
	riscv64-unknown-elf-gcc -march=rv64im -mabi=lp64 -static -mcmodel=medany -fvisibility=hidden -nostdlib -nostartfiles -I$(PWD)/common -T$(PWD)/common/link.ld test.S -o test.elf

disass: compile
	riscv64-unknown-elf-objdump -D test.elf > test.disass

spike: compile
	spike --isa=rv64im test.elf 
	spike --log-commits --log test_spike.dump --isa=rv64im +signature=test_spike_signature.log test.elf

clean:
	rm -rf *.elf *.disass *.log *.dump

```
