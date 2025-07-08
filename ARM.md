# ARM (Advanced RISC Machine)

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
- Phones Would Be Bigger or Battery-Hungry
  	- ARM processors save power.
  	- Without ARM, phones might need bigger batteries and would not last a full day.

- IoT and Smart Devices May Not Exist
	- Smart devices like fitness bands, smart bulbs, smart speakers rely on ARM’s small size and efficiency.
  	- Without ARM, many small devices might not even be possible.

- Mobile Performance Would Be Worse
	- ARM balances high performance with low power.
  	- Without ARM, mobile devices might use power-hungry processors that generate heat and quickly drain batteries.

- Less Affordable Devices
  	- ARM designs are licensed cheaply and are easy to produce.
  	- Without ARM, devices might become more expensive because alternatives could cost more to develop and manufacture.

---

## General Info
- ARM is a **32-bit RISC (Reduced Instruction Set Computer)** architecture.
- Widely used in **commercial products** like:
  -  Video game consoles  
  -  Modems  
  -  Mobile phones  
- Known for:
  -  Simplicity of architecture  
  -  Low power consumption  
  -  Small silicon area  

---

##  CISC vs RISC Comparison

| Feature            | CISC                                 | RISC                                      |
|--------------------|---------------------------------------|-------------------------------------------|
| Speed              | Slower                               | Faster / Competitive                      |
| Clock Cycles       | One instruction may take **multiple cycles** | One instruction per **clock cycle** |
| Development Cost   | More complex, expensive              | Simpler, cheaper to develop               |

---

##  RISC Architecture Key Features
- Large uniform **register files**
- **Load/store** architecture (data manipulation only in registers)
- **Simple addressing modes**
- **Fixed-length** instruction fields

---

##  ARM Architecture plus Enhancements
- Each instruction controls both **ALU** and **Barrel Shifter**
- **Auto-increment/decrement** addressing modes
- **Multiple load/store** support
- **Conditional execution** of instructions
- Based on **Berkeley RISC** machine

---

##  ARM Instruction Sets
ARM supports two types of instruction sets:
1. **32-bit ARM Instruction Set**
2. **16-bit Thumb Instruction Set** (improves code density)

---

##  Data Sizes in ARM

| Type        | Size              |
|-------------|-------------------|
| Byte        | 8 bits            |
| Half-word   | 16 bits (2 bytes) |
| Word        | 32 bits (4 bytes) |

---

##  Core Components of ARM Architecture
![image](https://github.com/user-attachments/assets/43ed6dad-4058-4427-be00-80d3d1c4ac13)

###  Register Bank
- Stores data for operations
- Connected to **ALU**

###  ALU (Arithmetic Logic Unit)
- Performs operations (add, subtract, etc.)
- Works with **Barrel Shifter** for fast execution
- Result is stored back in the register

###  Barrel Shifter
- Pre-processes data (shift/rotate left or right)
- Helps improve instruction speed
- Connected via **B-Bus**

###  A-Bus & B-Bus
- **A-Bus**: Direct path to ALU  
- **B-Bus**: Passes data through the **Barrel Shifter** to ALU

###  Program Counter (PC)
- Holds address of the **next instruction**
- Increments after each instruction

###  Instruction Decoder
- Decodes instructions before execution

###  Data Out Register
- Sends processed data to memory or peripherals

---

## 🔄 Load vs Store Operations

| Operation | Description                            |
|-----------|----------------------------------------|
| **Load**  | Copies data from **memory → register** |
| **Store** | Copies data from **register → memory** |

>  In ARM, **all manipulations must be done in registers**, not directly on memory.

---


# ARM REGISTERS
   ![image](https://github.com/user-attachments/assets/845dc995-f763-461f-b0ca-3f558ebbfb5c)
   
- In ARM, registers like R0, R1, R2, R3,..., R11 are the general purpose registers.
- They are typically used to:
	- Store data (like integers, memory addresses, function parameters).
	- Pass values between functions.
	- Perform arithmetic operations.
	- Carry and transfer data.
 
### Basic example
  -Generally, In arm we use assembly level language.
```
MOV R0, #5    ; Move the value 5 into register R0 (data)
ADD R1, R0, #3 ; Add 3 to the value in R0, result stored in R1
```
---

### INTRA PROCEDURAL CALL(IP):

| Feature        | Description                      |
|----------------|----------------------------------|
| NAME           |  IP Register (R12)               |
| TYPE           |   temporary register             |
| USAGE SCOPE    |   inside the same function       |
| PURPOSE        |   Temporary storage, scratch data for calculations, address computation, etc.|
| COMMON USE      |   compilers for fast local operations or by assembly for temp values|

- Intra-Procedural Call means a call that happens within the
  same function.
- It does not leave the current procedure and does not invoke
  other procedures.
  
- Jumps, loops, or internal control flows that happen inside
  the function boundaries.


**Example:**
- When doing intra-procedural operations like temporary calculations or internal jumps, the IP register can temporarily hold data.
  
```
ADD R12, R0, R1  ;  Store temp result in IP (R12)
SUB R2, R12, R3  ;   Use the temp result in further calculation
```
* R12 (IP) is used within the function only for temporary storage.
* It is not saved if another function is called.
---

## STACK POINTER(SP):

| Feature        | Description                      |
|----------------|----------------------------------|
| NAME           |  SP Register (R13)               |
| DIRECTION      |  Grows downwards                 |
| KEY ROLE       |  inside the same function        |
| PURPOSE        |  Tracks stack memory for function calls, local variables, return addresses|
| AUTOMATIC 
  UPDATE         |   PUSH/POP instructions auto-update SP|

The stack is used for:
- Storing local variables
- Passing function arguments
- Saving return addresses
 
The SP tells the processor where this stack data is located in memory.

In ARM architecture, the stack is typically full descending, which means:
- The stack grows downward (towards lower memory addresses).
- The SP points to the last pushed item on the stack.

#### What does the Stack Pointer (SP) exactly do?

The SP register:
- Is automatically updated when:
	- Data is pushed (stored) onto the stack ➜ SP decreases.
	- Data is popped (retrieved) from the stack ➜ SP increases.

- Push operation (store data)
      - PUSH {R0, R1, LR} ; Save registers R0, R1, and Link Register to the stack---SP is automatically decreased.
- Pop operation (retrieve data)
      - POP {R0, R1, LR} ; Restore the saved values from the stack---SP is automatically increased.

  ---
  
### LINK REGISTER(LR)

| Feature        | Description                      |
|----------------|----------------------------------|
| NAME                |   LR Register (R14)               |
| PURPOSE             |   Holds return address during function calls  |
| USAGE               |   inside the same function       |
| PURPOSE             |   BL stores the return address in LR, BX LR returns|
| DATA COMMOUNICATION |   LR passes the control flow back to the caller, not direct data like general-purpose registers do|

- It mainly holds the return address when a function (or subroutine) is called.
- LR is to know where to come back after a function is done.
- It helps manage program flow but is not used for data transfer between functions.
- Without LR, the program wouldn’t know how to come back after a function call in ARM.


**Different between GPR and LR**

| Aspect        | General-Purpose Registers          | Link Register (LR)  |
| ------------- | ---------------------------------- | ------------------- |
| Purpose       | Store and transfer **data**        | Store **return address**          |
| Usage         | Move, add, subtract, etc.          | Manage function calls and returns |
| Communication | Pass variables, function arguments | Pass the return location          |
| Example       | `MOV R0, #5`                       | `BL function` → `BX LR`           |

---
                                                                            
### PROGRAM COUNTER(PC)

| Feature             | Details                            |
| ------------------- | ---------------------------------- |
| Purpose             | Track next instruction             |
| Controls            | Program execution flow             |
| Data Role           | Does not carry data                |
| Affected by         | Branch, Jump, Function calls       |
| Automatic Increment | Usually by 4 bytes per instruction |

The Program Counter (PC) is a special-purpose register that holds the memory address of the next instruction the CPU will execute.
- In ARM architecture:
  	- The PC tells the CPU where to look next in memory.
  	- After executing one instruction, the PC automatically moves to the next
  	  instruction (normally increasing by 4 bytes because each ARM instruction
  	  is 4 bytes long in ARM state).
- It keeps track of the instruction flow.

**Example:**

| Step | PC Value | Instruction    |
| ---- | -------- | -------------- |
| 1    | 0x1000   | MOV R0, #5     |
| 2    | 0x1004   | ADD R1, R0, #3 |
| 3    | 0x1008   | BX LR          |

- After executing the instruction at 0x1000, the PC automatically moves to 0x1004 to fetch the next instruction.
- The PC does NOT carry or transfer data like general-purpose registers.
- The PC carries the address of instructions, not data values.

**Difference between LR and PC**

| Feature           | Link Register (LR)                                       | Program Counter (PC)                                      |
| ----------------- | -------------------------------------------------------- | --------------------------------------------------------- |
| **Register Name** | R14                                | R15      |
| **Purpose**       | Stores **return address** during function calls          | Stores the **address of the next instruction** to execute |
| **Role**          | Controls **where to return** after a function            | Controls **current execution location**                   |
| **Updates By**    | Set automatically by `BL` (Branch with Link) instruction | Updates automatically as each instruction is executed     |
| **Type of Flow**  | Manages return flow                                 | Manages program flow                                |
| **Used For**      | Function calls and exceptions                            | Every instruction fetch and execution                     |
| **Access**        | Can be read/written like other registers                 | Can be read/written but usually updated automatically     |
| **Example**       | `BL function` stores return address in LR                | PC always holds the current instruction address           |

---

#### CURRENT PROGRAM STATUS REGISTER(CSPR)

| Feature              | Description                               |
| -------------------- | ----------------------------------------- |
| Register Name        | CPSR (Current Program Status Register)    |
| Controls             | Status flags, processor mode, interrupts, instruction set |
| Key Flags            | N (Negative), Z (Zero), C (Carry), V (Overflow)  |
| Instruction Set Mode | ARM/Thumb, controlled by T bit           |
| Interrupt Control    | IRQ/FIQ enable/disable                   |


- When an interrupt come then ARM mode is changed.
- There are 7 modes in the ARM. User mode, system mode, supervisor mode, FIQ mode, IRQ mode, abort mode, undefined mode.
---
**CSPR key fields**

| Bits       | Name          | Purpose                                     |
| ---------- | ------------- | ------------------------------------------- |
| N (bit 31) | Negative Flag | Set if the result of an operation is negative |
| Z (bit 30) | Zero Flag     | Set if the result is zero                   |
| C (bit 29) | Carry Flag    | Set if there is a carry/borrow in arithmetic|
| V (bit 28) | Overflow Flag | Set if signed overflow occurs               |
| I (bit 7)  | IRQ Disable   | Disables IRQ interrupts when set            |
| F (bit 6)  | FIQ Disable   | Disables FIQ interrupts when set            |
| T (bit 5)  | Thumb State   | 1 = Thumb mode, 0 = ARM mode                |
| M\[4:0]    | Mode Bits     | Defines the processor mode                  |


**Status Reporting:**
        The CPSR tells whether the last operation resulted in zero, a negative number, overflow, or carry.
**Example 1: Zero Result**
```
assembly

MOV R0, #5
SUBS R1, R0, #5   ; R1 = 5 - 5 = 0
```
CPSR flags:
- Z = 1 (because result is 0)
- N = 0, C = 1, V = 0

**🔧 Example 2: Negative Result**
```
assembly

MOV R0, #5
SUBS R1, R0, #10   ; R1 = 5 - 10 = -5
```
CPSR flags:
-  Z = 0, V = 0
- N = 1 (result is negative)
- C = 0 (borrow occurred)

**🔧 Example 3: Carry Out (Unsigned Overflow)**
```
assembly

MOV R0, #0xFFFFFFFF
ADDS R1, R0, #1    ; R1 = 0xFFFFFFFF + 1 = 0x00000000
```
CPSR flags:

- Z = 1 (result is 0)
- C = 1 (carry occurred)
- N = 0, V = 0

**🔧 Example 4: Signed Overflow**
```
assembly

MOV R0, #0x7FFFFFFF   ; Largest positive signed int
ADDS R1, R0, #1       ; R1 = 0x80000000 → overflow into negative
```
CPSR flags:
- V = 1 (signed overflow)
- N = 1, Z = 0, C = 0
	
**Mode Control:**

- In ARM architecture, the processor can operate in different modes, which control:- what the processor can do, which          registers are accessible, how interrupts are handled.
- CPSR sets the processor’s operating mode (User, Supervisor, IRQ, etc.).
- M[4:0] refers to the bottom 5 bits (bits 0 to 4) in the CPSR (Current Program Status Register).
- These bits define the current processor mode.
- These bits tell the ARM processor which mode it is operating in.

| Mode Bits (M\[4:0]) | Processor Mode  | Description                      |
| ------------------- | --------------- | -------------------------------- |
| `10000` (0x10)      | User Mode       | Unprivileged mode (normal tasks) |
| `10001` (0x11)      | FIQ Mode        | Fast Interrupt handling mode     |
| `10010` (0x12)      | IRQ Mode        | Standard Interrupt handling mode |
| `10011` (0x13)      | Supervisor Mode | OS kernel mode (privileged)      |
| `10111` (0x17)      | Abort Mode      | Memory fault handling mode       |
| `11011` (0x1B)      | Undefined Mode  | Handles undefined instructions   |
| `11111` (0x1F)      | System Mode     | Privileged mode (used in OS)     |

- Bits [4:0] in the CPSR hold the current mode.
**Example:**
```
assembly

CPSR = 0x60000013  ; The mode bits (last 5 bits) are `10011` → Supervisor Mode

```
---

**Interrupt Management:**
- An interrupt is a signal that tells the processor to pause its current task and quickly handle something urgent.
- It enables or disables interrupt levels via the I (IRQ) and F (FIQ) bits.
- In ARM architecture, the processor can handle two types of hardware interrupts:
  	- IRQ (Normal Interrupt)
  	- FIQ (Fast Interrupt)
- Both are controlled by specific bits in the CPSR register.
  
| Term | Full Form              | Purpose                                |
| ---- | ---------------------- | -------------------------------------- |
| IRQ  | Interrupt Request      | Regular priority interrupt             |
| FIQ  | Fast Interrupt Request | High priority, fast response interrupt |

##### How it Works:
- If the I bit is set (1): IRQs are masked (blocked).
- If the I bit is cleared (0): IRQs are enabled (allowed to interrupt).
- If the F bit is set (1): FIQs are masked (blocked).
- If the F bit is cleared (0): FIQs are enabled (allowed to interrupt).
---

**Instruction Set State:**
In ARM architecture, the processor can operate in different instruction set states.
These states determine which type of instructions the processor will understand and execute.

The CPSR register’s T bit controls this.
The T bit in CPSR switches between ARM and Thumb instruction sets.
1. ARM State
- 32-bit instructions
- Full instruction set: Complex, powerful instructions.
- PC (Program Counter) usually increases by 4 bytes per instruction.
- T bit in CPSR = 0

2. Thumb State
- 16-bit instructions (more compact).
- Smaller code size, useful for low-memory systems.
- Limited instruction set compared to ARM mode.
- PC usually increases by 2 bytes per instruction.
- T bit in CPSR = 1

| State   | Instruction Size | T Bit in CPSR | Purpose                |
| ------- | ---------------- | ------------- | ---------------------- |
| ARM     | 32-bit           | 0             | Full feature set       |
| Thumb   | 16-bit           | 1             | Compact, faster access |
| Jazelle | Java Bytecode    | Special mode  | Java hardware support  |



