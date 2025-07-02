
### What is ARM?
```
- ARM stands for Advanced RISC Machine.
- It is a family of computer processors and architectures.
- Developed by ARM Holdings (originally Acorn Computers in the UK).
- ARM does not manufacture processors, it designs and licenses processor architectures to companies like Apple, Samsung, Qualcomm, etc.
```

### What is a Processor?

A processor, also known as a Central Processing Unit (CPU), is the brain of a computer or any computing device. It is the component responsible for executing instructions from programs by performing basic arithmetic, logical, control, and input/output (I/O) operations. It controls the flow of data in a system.














```
ARM--Advanced RISC Machine
used for commercial purpose
appli-----vedio games, modems, mobile phones
feactures---architecute simplicity
	    low power conception

cisc-- slower process and each instruction required one clock cycle
risc-- competitive easy to develop, cheap

architecture

risc-- large uniform register files
load or store arti
simple addressing modes
fixed length instruction fields

enhancement--each inst ctrl the alu and shifter
auto increment and decrement addressing modes
multiple load or store
conditional execution

high performace, low code size,low power consumption,low silicon area

based on the barkeley rics m/c
arn arch----fixed length instruct
supports pipelines concept
load and store archi-- using registor

it is 32 bit archi(address bus data bus)
  bytes---8bits
  word----32bits(4bytes)
  half word--16 bits(2bytes)

ARM's implement 2 types of instruction sets
	1. 32 bit arm instruction set
	2. 16 bit thumd instruction set



address register---indicates the address where to send the data
add increment-- next location
register bank
multiplier
shifter
ALU --perform operations with the help of barel shifter, in high speed and resukt is stored in the register bank form register bank the data is send out through the b bus and the data out register
data register
instruction decoder and control unit -- decodes the instuctions before the exectuin is done
pc bus-- next instruction to be performed, increment bus


registor bank which is connected to ALU has 2 data parts
1. a bus -- storing the data directly sending data to alu. 

2. b bus -- b bus to go alu via barel sifter which is also called as pre process 
 
alu is performing the process 
the data coming from any of this register is stored in the barel shifter with the help of b bus barel shifter can shift the data left or right or even rotate that is the barel shifer is doing some pre processing.

in this we have 2 registors rm and rn 
ex add 2 numbers one is send directly to the alu and the second is send to barel shifer so that it perform the any pre process as shifting the left bit or right bit and all that comes to alu from alu the data that is again send to register bank. 

from register bank the data is send to b bus as rd that is (result send to data out) throguth the b bus the data is sent to data out register and next to the data address

load---copies data from memory to register
store--copies data from register to memory 
in arm any manupation can be only done in the register
```




