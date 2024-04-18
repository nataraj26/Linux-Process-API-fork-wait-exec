# Ex02-OS-Linux-Process API - fork(), wait(), exec()

## Operating systems Lab exercise

## AIM :
To write C Program that uses Linux Process API - fork(), wait(), exec()

## DESIGN STEPS :

## Step 1 :

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

## Step 2 :

Write the C Program using Linux Process API - fork(), wait(), exec()

## Step 3 :

Test the C Program for the desired output.

## PROGRAM :


## DEVELOPED BY : NATARAJ KUMARAN S

## REG NO : 212223230137

### C Program to print process ID and parent Process ID using Linux API system calls :
```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{	//variable to store calling function's process id
	pid_t process_id;
	//variable to store parent function's process id
	pid_t p_process_id;
	//getpid() - will return process id of calling function
	process_id = getpid();
	//getppid() - will return process id of parent function
	p_process_id = getppid();
	//printing the process ids

//printing the process ids
	printf("The process id: %d\n",process_id);
	printf("The process id of parent function: %d\n",p_process_id);
	return 0; }
```
### OUTPUT :

![323450163-dd6c33f8-bcbb-4bf9-8021-d4ac75e57e1c](https://github.com/nataraj26/Linux-Process-API-fork-wait-exec/assets/147514615/a1517d1b-4674-4bc0-85cf-a937a6990110)

### C Program to create new process using Linux API system calls fork() and exit() :
~~~c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main() {
    int pid;
    pid = fork();
    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }
    else if (pid == 0) {
        printf("I am child, my pid is %d\n", getpid());
        printf("My parent pid is: %d\n", getppid());
        exit(EXIT_SUCCESS);
    }
    else {
        printf("I am parent, my pid is %d\n", getpid());
        sleep(100);
        exit(EXIT_SUCCESS);
    }
    return 0;
}
~~~
### OUTPUT :

![323450128-7d30e7ed-c75c-4147-8433-1e7973037993](https://github.com/nataraj26/Linux-Process-API-fork-wait-exec/assets/147514615/d1d4ad95-22e6-4827-adc5-571dcfe9f286)

### C Program to execute Linux system commands using Linux API system calls exec() family :
~~~c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
int main() {
    pid_t pid = fork();
    if (pid < 0) {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        printf("This is the child process. Executing 'ls' command.\n");
        execl("/bin/ls", "ls", "-l", NULL); // Lists files in long format
        perror("execl failed");
        exit(EXIT_FAILURE);
    } else {
        int status;
        waitpid(pid, &status, 0); // Wait for the child to finish
        if (WIFEXITED(status)) {
            printf("Child process exited with status %d.\n", WEXITSTATUS(status));
        } else {
            printf("Child process did not exit normally.\n");
        }
        printf("Parent process is done.\n");
    }
    return 0;
}
~~~
### OUTPUT :
![323450085-f5b88dc4-1374-4e4a-8e3f-98a53c5459d0](https://github.com/nataraj26/Linux-Process-API-fork-wait-exec/assets/147514615/6dfff6f2-088a-4beb-bfb1-684f66ceb0c4)

### RESULT :
Thus the programs are executed successfully.
