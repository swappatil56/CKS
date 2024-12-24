Strace intercecept the system calls of process
it display logs and received signals.


strace ls
strace {options}

-o filename
-v verbose
-f follow fork

-cw (count and summarize)
-p pid
-P path



controlplane $ strace cw -ls
strace: Can't stat 'cw': No such file or directory
controlplane $ strace -cw ls /
bin  boot  dev  etc  home  ks  lib  lib32  lib64  libx32  lost+found  media  mnt  opt  proc  root  run  sbin  snap  srv  swapfile  sys  tmp  usr  var
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 39.64    0.001180        1179         1           write
 17.98    0.000535          59         9           fstat
 14.53    0.000432          16        26           mmap
  4.87    0.000145         145         1           execve
  3.70    0.000110          13         8           mprotect
  3.67    0.000109          10        10           close
  3.50    0.000104          13         8           openat
  2.22    0.000066           9         7           read
  1.69    0.000050           6         8           pread64
  1.21    0.000036          18         2         2 statfs
  1.08    0.000032          16         2           getdents64
  1.06    0.000031          10         3           brk
  0.95    0.000028          28         1           munmap
  0.75    0.000022          11         2         2 access
  0.69    0.000021          10         2           ioctl
  0.58    0.000017           8         2           rt_sigaction
  0.43    0.000013           6         2         1 arch_prctl
  0.42    0.000013          12         1           stat
  0.27    0.000008           8         1           prlimit64
  0.27    0.000008           7         1           set_tid_address
  0.26    0.000008           7         1           rt_sigprocmask
  0.20    0.000006           6         1           set_robust_list
------ ----------- ----------- --------- --------- ----------------
100.00    0.002976                    99         5 total
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ echo hello > test
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ strace ls hello       
execve("/usr/bin/ls", ["ls", "hello"], 0x7ffc4657f188 /* 16 vars */) = 0
brk(NULL)                               = 0x55ea5ad97000
arch_prctl(0x3001 /* ARCH_??? */, 0x7fff70e76c20) = -1 EINVAL (Invalid argument)
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=65112, ...}) = 0
mmap(NULL, 65112, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f36d94f8000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0@p\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=163200, ...}) = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f36d94f6000
mmap(NULL, 174600, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f36d94cb000
mprotect(0x7f36d94d1000, 135168, PROT_NONE) = 0
mmap(0x7f36d94d1000, 102400, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x7f36d94d1000
mmap(0x7f36d94ea000, 28672, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1f000) = 0x7f36d94ea000
mmap(0x7f36d94f2000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x26000) = 0x7f36d94f2000
mmap(0x7f36d94f4000, 6664, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7f36d94f4000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\300A\2\0\0\0\0\0"..., 832) = 832
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
pread64(3, "\4\0\0\0\20\0\0\0\5\0\0\0GNU\0\2\0\0\300\4\0\0\0\3\0\0\0\0\0\0\0", 32, 848) = 32
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\7\2C\n\357_\243\335\2449\206V>\237\374\304"..., 68, 880) = 68
fstat(3, {st_mode=S_IFREG|0755, st_size=2029592, ...}) = 0
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
pread64(3, "\4\0\0\0\20\0\0\0\5\0\0\0GNU\0\2\0\0\300\4\0\0\0\3\0\0\0\0\0\0\0", 32, 848) = 32
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\7\2C\n\357_\243\335\2449\206V>\237\374\304"..., 68, 880) = 68
mmap(NULL, 2037344, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f36d92d9000
mmap(0x7f36d92fb000, 1540096, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x22000) = 0x7f36d92fb000
mmap(0x7f36d9473000, 319488, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x19a000) = 0x7f36d9473000
mmap(0x7f36d94c1000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1e7000) = 0x7f36d94c1000
mmap(0x7f36d94c7000, 13920, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7f36d94c7000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\340\"\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=588488, ...}) = 0
mmap(NULL, 590632, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f36d9248000
mmap(0x7f36d924a000, 413696, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x2000) = 0x7f36d924a000
mmap(0x7f36d92af000, 163840, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x67000) = 0x7f36d92af000
mmap(0x7f36d92d7000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x8e000) = 0x7f36d92d7000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libdl.so.2", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0 \22\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=18848, ...}) = 0
mmap(NULL, 20752, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f36d9242000
mmap(0x7f36d9243000, 8192, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1000) = 0x7f36d9243000
mmap(0x7f36d9245000, 4096, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7f36d9245000
mmap(0x7f36d9246000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7f36d9246000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpthread.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220q\0\0\0\0\0\0"..., 832) = 832
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\232e\273F\236E\241\306\373\317\372\345\270*/\327"..., 68, 824) = 68
fstat(3, {st_mode=S_IFREG|0755, st_size=157224, ...}) = 0
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\232e\273F\236E\241\306\373\317\372\345\270*/\327"..., 68, 824) = 68
mmap(NULL, 140408, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f36d921f000
mmap(0x7f36d9225000, 69632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x7f36d9225000
mmap(0x7f36d9236000, 24576, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x17000) = 0x7f36d9236000
mmap(0x7f36d923c000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1c000) = 0x7f36d923c000
mmap(0x7f36d923e000, 13432, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7f36d923e000
close(3)                                = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f36d921d000
arch_prctl(ARCH_SET_FS, 0x7f36d921e400) = 0
mprotect(0x7f36d94c1000, 16384, PROT_READ) = 0
mprotect(0x7f36d923c000, 4096, PROT_READ) = 0
mprotect(0x7f36d9246000, 4096, PROT_READ) = 0
mprotect(0x7f36d92d7000, 4096, PROT_READ) = 0
mprotect(0x7f36d94f2000, 4096, PROT_READ) = 0
mprotect(0x55ea5abc8000, 4096, PROT_READ) = 0
mprotect(0x7f36d9535000, 4096, PROT_READ) = 0
munmap(0x7f36d94f8000, 65112)           = 0
set_tid_address(0x7f36d921e6d0)         = 11014
set_robust_list(0x7f36d921e6e0, 24)     = 0
rt_sigaction(SIGRTMIN, {sa_handler=0x7f36d9225bf0, sa_mask=[], sa_flags=SA_RESTORER|SA_SIGINFO, sa_restorer=0x7f36d9233420}, NULL, 8) = 0
rt_sigaction(SIGRT_1, {sa_handler=0x7f36d9225c90, sa_mask=[], sa_flags=SA_RESTORER|SA_RESTART|SA_SIGINFO, sa_restorer=0x7f36d9233420}, NULL, 8) = 0
rt_sigprocmask(SIG_UNBLOCK, [RTMIN RT_1], NULL, 8) = 0
prlimit64(0, RLIMIT_STACK, NULL, {rlim_cur=8192*1024, rlim_max=RLIM64_INFINITY}) = 0
statfs("/sys/fs/selinux", 0x7fff70e76b70) = -1 ENOENT (No such file or directory)
statfs("/selinux", 0x7fff70e76b70)      = -1 ENOENT (No such file or directory)
brk(NULL)                               = 0x55ea5ad97000
brk(0x55ea5adb8000)                     = 0x55ea5adb8000
openat(AT_FDCWD, "/proc/filesystems", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0444, st_size=0, ...}) = 0
read(3, "nodev\tsysfs\nnodev\ttmpfs\nnodev\tbd"..., 1024) = 410
read(3, "", 1024)                       = 0
close(3)                                = 0
access("/etc/selinux/config", F_OK)     = -1 ENOENT (No such file or directory)
ioctl(1, TCGETS, {B38400 opost isig icanon echo ...}) = 0
ioctl(1, TIOCGWINSZ, {ws_row=49, ws_col=187, ws_xpixel=0, ws_ypixel=0}) = 0
stat("hello", 0x55ea5ad97a88)           = -1 ENOENT (No such file or directory)
lstat("hello", 0x55ea5ad97a88)          = -1 ENOENT (No such file or directory)
write(2, "ls: ", 4ls: )                     = 4
write(2, "cannot access 'hello'", 21cannot access 'hello')   = 21
write(2, ": No such file or directory", 27: No such file or directory) = 27
write(2, "\n", 1
)                       = 1
close(1)                                = 0
close(2)                                = 0
exit_group(2)                           = ?
+++ exited with 2 +++
controlplane $ 



###################################################################################################

Lab


controlplane $ strace -cw kill -9 1234    
kill: (1234): No such process
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 27.17    0.000241           4        49           mmap
 15.95    0.000141          35         4           write
 10.43    0.000092          92         1           execve
 10.28    0.000091           6        15           openat
  7.58    0.000067           5        13           mprotect
  6.69    0.000059           3        17           close
  6.35    0.000056           4        14           read
  5.22    0.000046           3        14           fstat
  3.40    0.000030           3         8           pread64
  1.31    0.000012           3         3           brk
  1.22    0.000011          10         1           munmap
  0.83    0.000007           3         2         1 arch_prctl
  0.70    0.000006           3         2           rt_sigaction
  0.68    0.000006           5         1         1 access
  0.42    0.000004           3         1         1 kill
  0.38    0.000003           3         1           prlimit64
  0.35    0.000003           3         1           rt_sigprocmask
  0.35    0.000003           3         1           set_robust_list
  0.34    0.000003           2         1           getpid
  0.33    0.000003           2         1           set_tid_address
------ ----------- ----------- --------- --------- ----------------
100.00    0.000886                   150         3 total
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ strace -cw kill -15 1234
kill: (1234): No such process
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 28.99    0.000290           5        49           mmap
 14.53    0.000145         145         1           execve
 12.70    0.000127          31         4           write
 10.17    0.000102           6        15           openat
  6.68    0.000067           5        13           mprotect
  6.17    0.000062           4        14           read
  6.11    0.000061           3        17           close
  5.34    0.000053           3        14           fstat
  2.77    0.000028           3         8           pread64
  1.18    0.000012           3         3           brk
  1.06    0.000011          10         1           munmap
  0.82    0.000008           4         2         1 arch_prctl
  0.69    0.000007           6         1         1 access
  0.68    0.000007           3         2           rt_sigaction
  0.40    0.000004           4         1         1 kill
  0.40    0.000004           3         1           rt_sigprocmask
  0.35    0.000003           3         1           set_robust_list
  0.34    0.000003           3         1           prlimit64
  0.31    0.000003           3         1           set_tid_address
  0.31    0.000003           3         1           getpid
------ ----------- ----------- --------- --------- ----------------
100.00    0.000999                   150         3 total
controlplane $ 
controlplane $ strace -cw uname 
Linux
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 61.48    0.000612         612         1           execve
 13.87    0.000138         138         1           write
  6.13    0.000061          10         6           pread64
  5.19    0.000052           7         7           mmap
  2.30    0.000023           7         3           mprotect
  1.96    0.000020           4         4           close
  1.68    0.000017           8         2           openat
  1.66    0.000017           5         3           fstat
  1.54    0.000015           5         3           brk
  1.20    0.000012          11         1           munmap
  0.94    0.000009           4         2         1 arch_prctl
  0.93    0.000009           9         1         1 access
  0.63    0.000006           6         1           read
  0.49    0.000005           4         1           uname
------ ----------- ----------- --------- --------- ----------------
100.00    0.000996                    36         2 total
controlplane $ 
controlplane $ 
controlplane $ strace -cw nc -l -p 8080


^Cstrace: Process 15812 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 99.99   27.494884    27494883         1         1 accept4
  0.01    0.001780        1780         1           execve
  0.00    0.000530         132         4           openat
  0.00    0.000082           4        18           mmap
  0.00    0.000030           4         6           mprotect
  0.00    0.000018           2         6           pread64
  0.00    0.000014           4         3           brk
  0.00    0.000013           3         4           fstat
  0.00    0.000012           4         3           read
  0.00    0.000012           2         4           close
  0.00    0.000011          11         1           socket
  0.00    0.000010           4         2           setsockopt
  0.00    0.000008           8         1           munmap
  0.00    0.000008           3         2         1 arch_prctl
  0.00    0.000007           7         1         1 access
  0.00    0.000007           6         1           bind
  0.00    0.000005           4         1           listen
  0.00    0.000004           3         1           rt_sigaction
------ ----------- ----------- --------- --------- ----------------
100.00   27.497433                    60         3 total

controlplane $ 



que: Use strace to see what kind of syscalls the kube-apiserver process performs.



controlplane $ strace -p 1899 -f -cw
strace: Process 1899 attached with 7 threads
^Cstrace: Process 1899 detached
strace: Process 1946 detached
strace: Process 1947 detached
strace: Process 1972 detached
strace: Process 1973 detached
strace: Process 1974 detached
strace: Process 4147 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 67.10    7.791423       12061       646       286 futex
 28.13    3.265627        2705      1207           epoll_pwait
  4.37    0.507633         320      1586           nanosleep
  0.18    0.021278         170       125           write
  0.08    0.009296        9295         1         1 restart_syscall
  0.07    0.008554         131        65           sched_yield
  0.04    0.004984          19       254       122 read
  0.00    0.000445          37        12           rt_sigreturn
  0.00    0.000385          96         4           close
  0.00    0.000351          13        26           getrandom
  0.00    0.000261           9        28           setsockopt
  0.00    0.000213          17        12           tgkill
  0.00    0.000164          20         8         4 accept4
  0.00    0.000139          11        12           getpid
  0.00    0.000094          11         8           epoll_ctl
  0.00    0.000047          11         4           getsockname
  0.00    0.000017          16         1           uname
------ ----------- ----------- --------- --------- ----------------
100.00   11.610910                  3999       413 total
