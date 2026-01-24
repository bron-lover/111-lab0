# A Kernel Seedling

This lab implements a kernel module that produces a /proc/count file that when read returns the current number of running processes. We needed to implement a kernal module because you cannot access information such as the number of running processes through a normal user-space program. Exposing this inofrmation can only be done by a program that runs inside the kernel. To actually implement this functionality, I initialized a task_struct variable combined with for_each_process to iterate through all active processes, incremeting a count variable each time. Then I used seq_printf to write this number into the /proc directory.

## Building
```shell
make
```

## Running
```shell
sudo insmod proc_count.ko
cat /proc/count
```
Results (in stdout):

150

## Cleaning Up
```shell
sudo rmmod proc_count
make clean
```

## Testing
```python
python -m unittest
```
Results (in stdout):

Ran 3 tests in 33.243s

OK

Report which kernel release version you tested your module on
(hint: use `uname`, check for options with `man uname`).
It should match release numbers as seen on https://www.kernel.org/.

```shell
uname -r -s -v
```
Kernel Version:

Linux 5.14.8-arch1-1 #1 SMP PREEMPT Sun, 26 Sep 2021 19:35:15 +0000
