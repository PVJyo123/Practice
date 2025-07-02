
-Explain the concept of process creation in operating systems. 

-Differentiate between the fork() and exec() system calls. 
### Write a C program to demonstrate the use of fork() system call.
```
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<stdlib.h>

int main()
{
        pid_t pid;
        pid=fork();
        if(pid<0)
        {
                printf("not created");
                exit(1);
        }
        else if(pid==0)
        {
                printf("\nthis is in the child class\n");
        }
        else
        {
                printf("\nthis is parent class\n");
        }
}
```
-What is the purpose of the wait() system call in process management? 

-Describe the role of the exec() family of functions in process management. 

### Write a C program to illustrate the use of the execvp() function. 
```
#include<stdio.h>
#include<sys/types.h>
#include<unistd.h>
void main()
{
        printf("this is example of execvp system call\n");
        char *args[]={"ls","-l",NULL};
        execvp("ls",args);
        printf("this printf never appers\n");
}
```
How does the vfork() system call differ from fork()? 

Discuss the significance of the getpid() and getppid() system calls. 

Explain the concept of process termination in UNIX-like operating systems. 

### Write a program in C to create a child process using fork() and print its PID.
```
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<stdlib.h>

int main()
{
        pid_t pid;
        pid=fork();
        if(pid<0)
        {
                printf("not created");
                exit(1);
        }
        else if(pid==0)
        {
                printf("this is in the child class\n");
        }
        else
        {
                printf("this is parent class\n");
		printf("pid is:%d",pid);
        }
}
 ```
Describe the process hierarchy in UNIX-like operating systems.

What is the purpose of the exit() function in C programming? 

### Explain how the execve() system call works and provide a code example.
```
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/types.h>

int main()
{
	 printf("this is example of execve system call\n");
        char *args[]={"/bin/ls","-l", "/home", NULL};
	char *env[]={NULL};
        if(execve("/bin/ls",args, env)==-1)
	   printf("failed\n");
        printf("this printf never appers\n");
}
 
ls is replaced with /bin/ls
```
Discuss the role of the fork() system call in implementing multitasking. 

### Write a C program to create multiple child processes using fork() and display their PIDs. 
```
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/wait.h>

int main()
{
        int pid,i;
        for(i=0;i<5;i++)
        {
        pid=fork();
        if(pid<0)
        {
                printf("failed");
                return 0;
        }
        else if(pid==0)
          {
		printf("child %d: my pid is %d, parent pid is %d\n",i+1,getpid(),getppid());
                exit(0);
          }
        }
        for(i=0;i<5;i++)
        {
                wait(NULL);
        }
        printf("parent: all child process completed\n");
        return 0;
}
```
How does the exec() system call replace the current process image with a new one? 

Explain the concept of process scheduling in operating systems. 

Describe the role of the clone() system call in process management. 

### Write a program in C to create a zombie process and explain how to avoid it. 
```
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/wait.h>

int main()
{
	int pid;
	pid=fork();
	if(pid==0)
	  {
		printf("child process %d is exiting.\n",getpid());
		exit(0);
	  }
	else
	  {
		printf("parent process(PID:%d) is sleeping. child PID:%d\n",pid);
		sleep(20);
		printf("parent process is now exiting.\n");

	}
}

the parent process reads the child’s exit status.(wait() or waitpid() in parent process)
The kernel automatically cleans up child processes if you tell it to ignore SIGCHLD(signal(SIGCHLD, SIG_IGN);)
```
Discuss the significance of the setuid() and setgid() system calls in process man 

Explain the concept of process groups and their significance in UNIX-like operating systems. 

### Write a C program to demonstrate the use of the waitpid() function for process synchronization. 
```
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/wait.h>

int main()
{
	int pid1,pid2,wpid,stat;
	pid1=fork();
	if(pid1<0)
		printf("failed");
	else if(pid1==0)
	  {
		printf("child 1 PID=%d, Parent PID=%d\n",getpid(),getppid());
		sleep(5);
		printf("child 1:existing\n");
		exit(1);
	  }

	pid2=fork();
	if(pid2<0)
		printf("failed");
	else if(pid2==0)
	  {
		printf("child 2 PID=%d, Parent PID=%d\n",getpid(),getppid());
		sleep(2);
		printf("child 2:existing\n");
		exit(2);
	  }

	wpid=waitpid(pid2,&stat,0);
	if(WIFEXITED(stat))
		printf("parent: child 2 with pid %d exited with status %d\n",wpid,WEXITSTATUS(stat));
	
	wpid=waitpid(pid1,&stat,0);
	if(WIFEXITED(stat))
		printf("parent: child 1 with pid %d exited with status %d\n",wpid,WEXITSTATUS(stat));
	printf("parent : all child processes completed.\n")
}
```
Discuss the role of the execle() function in the exec() family of calls. 

Describe the purpose of the nice() system call in process scheduling.

### Write a program in C to create a daemon process. 
```
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/wait.h>

int main()
{
	int pid;
	pid=fork();
	if(pid<0)
	  {
		printf("failed");
		exit(1);
	  }
	if(pid>0)
	  {
		printf("parent process exiting.Deamon process PID:%d\n",pid);
		exit(0);
	  }
while(1)
{
  	FILE *fp=fopen("/tmp/simple_deamon_log.txt","a+");
if(fp)
{
printf("Deamon is running.PID:%d\n",getpid());
}
sleep(5);
}}

after running this code this will be in continous child process in backgroud.
to see the child process we use ps -p 1988.
   PID TTY          TIME CMD
   2031 pts/0    00:00:00 a.out
to stop this we need to kill this child process kill pid(kill 1988).
```
Explain the role of the getpid() and getppid() functions in process management. 

Discuss the difference between the fork() and clone() system calls. 

### Write a C program to demonstrate the use of the system() function for executing shell commands. 
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
int ret;
ret=system("Date");
ret=system("mkdir shell_file");
if(ret=-1)
	printf("failed");
}

system() function in C is a library function used to execute shell commands directly from a C program.
 Shell commands control the OS through the terminal
```
-Explain the concept of process states in UNIX-like operating systems. 

-Describe the purpose of the chroot() system call and provide an example.agement.



