### What is a Processor?
```
A processor, also known as a Central Processing Unit (CPU), is the brain of a computer or any computing
device.
- It is the component responsible for executing instructions from programsby performing basic
  arithmetic, logical, control, and input/output (I/O) operations.
- It controls the flow of data in a system.

- A processor runs based on the instruction cycle (fetch-decode-execute-store):
```

### waht is RISC
```
- RISC (Reduced Instruction Set Computer) is a CPU architecture design.
- RISC was developed to improve CPU speed and efficiency.
- Earlier CPUs used CISC (Complex Instruction Set Computer), which had many complex instructions but took
  more clock cycles to execute.
- RISC was a simplification approach: Instead of making instructions powerful, make them simple but fast.
```

### What is ARM?
```
- ARM stands for Advanced RISC Machine.
- It is a family of computer processors and architectures.
- Developed by ARM Holdings (originally Acorn Computers in the UK).
- ARM does not manufacture processors; it designs and licenses processor architectures
  to companies like Apple, Samsung, Qualcomm, etc.
        -- Apple’s M1, M2, A15 processors → ARM-based.
        -- Qualcomm Snapdragon processors → ARM-based.
        -- Samsung Exynos processors → ARM-based.
```

### What Happens If We Don’t Have ARM?
```
🔸Phones Would Be Bigger or Battery-Hungry
ARM processors save power.

Without ARM, phones might need bigger batteries and would not last a full day.

🔸IoT and Smart Devices May Not Exist
Smart devices like fitness bands, smart bulbs, smart speakers rely on ARM’s small size and efficiency.

Without ARM, many small devices might not even be possible.

🔸Mobile Performance Would Be Worse
ARM balances high performance with low power.

Without ARM, mobile devices might use power-hungry processors that generate heat and quickly drain batteries.

🔸 Less Affordable Devices
ARM designs are licensed cheaply and are easy to produce.

Without ARM, devices might become more expensive because alternatives could cost more to develop and manufacture.
```








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
arm arch----fixed length instruct
supports pipelines concept
load and store archi-- using registor

it is 32 bit archi(address bus data bus)
  bytes---8bits
  word----32bits(4bytes)(speed to communicate)
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






```
Feature	Explanation
Name	IP Register (R12)
Type	temporary register
Usage Scope	inside the same function
Purpose	Temporary storage, scratch data for calculations, address computation, etc.
Common Use	By compilers for fast local operations or by assembly for temp values


Feature	Explanation
Register Number	R13 in ARM
Stack Direction	Typically full descending (grows downward)
Key Role	Tracks stack memory for function calls, local variables, return addresses
Communication Role	Passes data between functions, saves/restores register states
Automatic Updates	PUSH/POP instructions auto-update SP

The stack is used for:
•	Storing local variables
•	Passing function arguments
•	Saving return addresses
•	Saving processor state during interrupts or function calls (context switching)
The SP tells the processor where this stack data is located in memory.

In ARM architecture, the stack is typically full descending, which means:
•	The stack grows downward (towards lower memory addresses).
•	The SP points to the last pushed item on the stack.
What does the Stack Pointer (SP) exactly do?
The SP register:
•	Keeps track of the top of the stack.
•	Is automatically updated when:
o	Data is pushed (stored) onto the stack ➜ SP decreases.
o	Data is popped (retrieved) from the stack ➜ SP increases.
Push operation (store data)
PUSH {R0, R1, LR} ; Save registers R0, R1, and Link Register to the stack---SP is automatically decreased.
Pop operation (retrieve data)
POP {R0, R1, LR} ; Restore the saved values from the stack---SP is automatically increased.


Feature	Explanation
Purpose	Holds return address during function calls
Register Name	R14
Instruction used	BL stores the return address in LR, BX LR returns
Data communication	LR passes the control flow back to the caller, not direct data like general-purpose registers do.
 
It mainly holds the return address when a function (or subroutine) is called.
LR (Link Register) is like a bookmark to know where to come back after a function is done.
It helps manage program flow but is not used for data transfer between functions.
Without LR, the program wouldn’t know how to come back after a function call in ARM.

What General-Purpose Registers Do (Data Movement)
In ARM, registers like R0, R1, R2, R3, etc. are typically used to:
•	Store data (like integers, memory addresses, function parameters).
•	Pass values between functions.
•	Perform arithmetic operations.
MOV R0, #5    ; Move the value 5 into register R0 (data)
ADD R1, R0, #3 ; Add 3 to the value in R0, result stored in R1

What the Link Register Does (Control Flow)
The Link Register (LR) is not used to carry data like general-purpose registers.
Instead:
•	It holds the memory address of where the program should go back to after a function finishes.
•	This is about program flow — it’s like saying:
“When you are done here, continue from this address.”
•	LR controls where to go next.
•	It does not carry or transfer any variable or computation result. It simply tells the CPU:
“Jump to this location and continue execution.”

Feature	Details
Purpose	Track next instruction
Controls	Program execution flow
Data Role	Does not carry data
Affected by	Branch, Jump, Function calls
Automatic Increment	Usually by 4 bytes per instruction

The Program Counter (PC) is a special-purpose register that holds the memory address of the next instruction the CPU will execute.
In ARM architecture:
•	The PC tells the CPU where to look next in memory.
•	After executing one instruction, the PC automatically moves to the next instruction (normally increasing by 4 bytes because each ARM instruction is 4 bytes long in ARM state).
It keeps track of the instruction flow.
Example:
Step	PC Value	Instruction
1	0x1000	MOV R0, #5
2	0x1004	ADD R1, R0, #3
3	0x1008	BX LR
After executing the instruction at 0x1000, the PC automatically moves to 0x1004 to fetch the next instruction.
The PC does NOT carry or transfer data like general-purpose registers.
The PC carries the address of instructions, not data values.
It controls which instruction is executed next (this is called control flow, not data flow).

Feature	Description
Register Name	CPSR (Current Program Status Register)
Controls	Status flags, processor mode, interrupts, instruction set
Key Flags	N (Negative), Z (Zero), C (Carry), V (Overflow)
Instruction Set Mode	ARM/Thumb, controlled by T bit
Interrupt Control	IRQ/FIQ enable/disable

Bits	Name	Purpose
N (bit 31)	Negative Flag	Set if the result of an operation is negative
Z (bit 30)	Zero Flag	Set if the result is zero
C (bit 29)	Carry Flag	Set if there is a carry/borrow in arithmetic
V (bit 28)	Overflow Flag	Set if signed overflow occurs
I (bit 7)	IRQ Disable	Disables IRQ interrupts when set
F (bit 6)	FIQ Disable	Disables FIQ interrupts when set
T (bit 5)	Thumb State	1 = Thumb mode, 0 = ARM mode
M[4:0]	Mode Bits	Defines the processor mode

Status Reporting:
The CPSR tells whether the last operation resulted in zero, a negative number, overflow, or carry.
Mode Control:
CPSR sets the processor’s operating mode (User, Supervisor, IRQ, etc.).
M[4:0] refers to the bottom 5 bits (bits 0 to 4) in the CPSR (Current Program Status Register).
These bits define the current processor mode.
These bits tell the ARM processor which mode it is operating in.

Mode Bits (M[4:0])	Processor Mode	Description	
10000 (0x10)	User Mode	Unprivileged mode (normal tasks)	
10001 (0x11)	FIQ Mode	Fast Interrupt handling mode	
10010 (0x12)	IRQ Mode	Standard Interrupt handling mode	
10011 (0x13)	Supervisor Mode	OS kernel mode (privileged)	
10111 (0x17)	Abort Mode	Memory fault handling mode	
11011 (0x1B)	Undefined Mode	Handles undefined instructions	
11111 (0x1F)	System Mode	Privileged mode (used in OS)	

Interrupt Management:
It enables or disables interrupt levels via the I (IRQ) and F (FIQ) bits.
In ARM architecture, the processor can handle two types of hardware interrupts:
•	IRQ (Normal Interrupt)
•	FIQ (Fast Interrupt)
Both are controlled by specific bits in the CPSR register.
An interrupt is a signal that tells the processor to pause its current task and quickly handle something urgent.
Type	Full Form	Priority	Usage
IRQ	Interrupt Request	Lower	General interrupts
FIQ	Fast Interrupt Request	Higher	Time-critical events

How it Works:
•	If the I bit is set (1): IRQs are masked (blocked).
•	If the I bit is cleared (0): IRQs are enabled (allowed to interrupt).
•	If the F bit is set (1): FIQs are masked (blocked).
•	If the F bit is cleared (0): FIQs are enabled (allowed to interrupt).

Instruction Set State:
The T bit in CPSR switches between ARM and Thumb instruction sets.
1. ARM State
•	32-bit instructions
•	Full instruction set: Complex, powerful instructions.
•	PC (Program Counter) usually increases by 4 bytes per instruction.
•	T bit in CPSR = 0
2. Thumb State
•	16-bit instructions (more compact).
•	Smaller code size, useful for low-memory systems.
•	Limited instruction set compared to ARM mode.
•	PC usually increases by 2 bytes per instruction.
•	T bit in CPSR = 1

State	Instruction Size	T Bit in CPSR	Purpose
ARM	32-bit	0	Full feature set
Thumb	16-bit	1	Compact, faster access
Jazelle	Java Bytecode	Special mode	Java hardware support





