## Process and Thread Management in Linux

### What is a Process?

* A **process** is a running instance of a program
                    (or)
* program that is running in the user space of the RAM
* It runs in **user space** of RAM.
* When we execute, the contents of an executable file are loaded from
  hard disk into user space of RAM.

Example:

```
gcc file.c   -->   ./a.out   -->| text | --> user space of RAM
                                | data |
                                | bss  |
```

* Memory Segments: text, data, bss, heap, and stack.
* for every process memory segments are allocated in user space of RAM where as
  PCB is allocated in kernel space of RAM.
* **Process Control Block (PCB)** is created in **kernel space**.
* for every process there will be a unique PCB in kernal space of RAM. 

### PCB Contains:
```
* Process ID (PID)

* Parent Process ID (PPID)

* File Descriptor Table

* Signal Disposition Table

* Page Table

* Program Counter

* User ID

* Group ID
```

* All PCBs are linked as nodes in a linked list, managed by the **Process Management System**.
  
* Schedulers will have the access to the entire linked list.

* Scheduler schedules the PCB list to decide the next process to run.
  
## Process Scheduling

**how will it decide which program will be run next?**

We can tell it depends on scheduling mechanisms. Primarily, we have two. they are:

  - 1.Round Robin Scheduling
  - 2.Preemptive Priority Scheduling

### 1. Round Robin Scheduling 

* Equal CPU time for each process for execution.
* After the complition of last, scheduler jumps to the first.
* **Adv:**   - Has equal share of time,
              - no process starvation(wait).
  
* **Disadv:**   - No priority handling.

### 2. Preemptive Priority Scheduling 

* High-priority task preempts lower-priority task.
      - preemptive: performed by priority values. Highest priority will execute first.
  
* **Adv:** Important tasks run first.
* **Disadv:** Starvation of low-priority tasks.

**Context Switching**: Switching between processes.

## Parent and Child Processes

* Process that creates another process using fork() or exec().
* Child is a copy of parent process created using fork()
* It is an independent copy of the parent.

### `fork()`

* Fork() system call is used to create a new process within the process.
* The New process is called as child process and the old process is called as Parent process.

* when we invoke fork() it returns twice once in parent process and once in child Process.

* In parent process fork() returns child PID where as in child process fork() returns 0.
**Example**

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();
    if (pid == 0)
        printf("Child process\n");
    else
        printf("Parent process\n");
}
```

* Returns twice: once in parent (returns child PID), once in child (returns 0).

### `exec()` Family

* `execl`, `execv`, `execlp`, `execvp` these are the differnt types. 
* Replaces current process image with a new one.
* On success, the old code is **replaced**.
  ** syntax**
```
Execl (const char* path, const char* arg, ...., NULL)
```
**Example**
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    printf("This is an example of execl system call \n");
    execl("/bin/ls", "ls", "-l", NULL);
    printf("This print never appears in");
    return 0;
}
```

### Daemon

* Background process that runs independently. and is detached from terminal.

### Zombie

* Parent process Completed execution but not removed from process table (parent hasn't read exit status).

```c
#include <stdio.h>
#include <unistd.h>

int main
{
int pid;
 pid = fork();
if (pid > 0)
{
    printf("Parent process (PID: %d), sleeping...\n", getpid());
    sleep(30); // parent sleeps
}
else if(pid==0)
{
     printf("Child process (PID: %d) exiting...\n", getpid());
    exit(0);   // child exits
}
else
    printf("error");
}

```

**Output**: 
      * Parent process (PID: 6613), sleeping....
      
      * Child process (PID: 6617) exiting.......
 
### Orphan

* Parent exits before child.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() 
{
    int pid = fork();
    if (pid > 0)
   {
        printf("Parent process (PID: %d) exiting...\n", getpid()); 
        exit(0);  // Parent exits immediately
    }
   else if (pid == 0)
    {
        sleep(2);  // Give time for parent to exit
        printf("Child process (PID: %d), new parent PID: %d\n", getpid(), getppid());
        sleep(20); // Stay alive to observe in ps
    } 
    else
    {
        perror("fork");
    }

    return 0;
}

```
**Output**:  Parent process (PID: 5923) exiting....

---

## What is a Thread?

* **Parallelly executing functions** inside a process.
* **Lightweight process**, sharing the same PCB.
* Created using **Pthreads library**.

### Characteristics:

* Main thread: the initial thread created by `main()`.
* Threads share **heap**, **data**, and **bss**, but each has its own **stack**.
* Managed in **user space** by Pthread.

### CPU Thread Scheduling

* Switches thread when:

  1. Thread completes execution
  2. CPU time expires
```
  Void *thread function (void*args)
    {
    }
```

pthread_Create is a library function it is given by pthread library.
```
pthread_create(&ti, NULL, thread_fun, NULL);
```
*ti---thread identifier

*attr---base address of thread attributes.

*function--- fun ptr, base address of fun that needs to be created as thread.

*args---arguments passed to the thread.

- on Success pthread_create returns 0.
- on failure pthread_create returns non zero error number.


### Creating a Thread:

```c
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

void* thread_func(void* args) {
    for (int i = 0; i < 10; ++i) {
        printf("Thread function\n");
        sleep(1);
    }
    return NULL;
}

int main() {
    pthread_t ti;
    pthread_create(&ti, NULL, thread_func, NULL);
    for (int i = 0; i < 10; ++i) {
        printf("Main thread\n");
        sleep(1);
    }
    return 0;
}
```

### Compilation

```bash
gcc file.c -pthread
```

---

## Comparison Table

| Feature                          | **Process**                                                   | **Thread**                                                         |
| -------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Execution Context**            | Executes independently                                        | Executes as a part of the process                                  |
| **PCB (Process Control Block)**  | Has its **own PCB** maintained by the kernel                  | Shares the **same PCB** with other threads in the process          |
| **Memory Segments (User Space)** | May or may not share memory (usually isolated memory space)   | Shares **heap**, **data**, and **BSS** segments with other threads |
| **Memory Isolation**             | Isolated memory for each process                              | Threads **share** memory within the process                        |
| **Management**                   | Managed by the **Process Management Subsystem** in the kernel | Managed via the **Pthreads library** (user space thread API)       |
| **Stack Allocation**             | Each process has its **own stack** in user space              | Each thread has its **own stack** in user space                    |
| **Process Image Location**       | Entire **process image** resides in user space                | Threads share the **process image** except for individual stacks   |

---

**End of Document**
