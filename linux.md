## 查看linux系统进程的详细信息，比如执行文件路径，环境变量等
1. 找到pid，例如525
2. ls /proc/525
例如 cat /proc/525/environ
    ls -lh /proc/525/cwd
    
## 查看占用某端口的进程
netstat -lntp | grep 80
    
## 查看进程CPU、内存消耗
top -p 进程ID
其中RES为内存消耗，%CPU为CPU消耗

