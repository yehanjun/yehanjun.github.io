Linux 命令

netstat -tunlp | grep # 端口号，用于查看指定的端口号的进程情况，如查看80端口的情况
cp /dev/null filename 或者 cat /dev/null > filename #清空文件内容
nohup ./program >/dev/null 2>log & #只输出错误信息到日志文件
nohup ./program >/dev/null 2>&1 & #什么信息也不要
ps -ef | grep tail | grep -v grep | awk '{print $2}' | xargs kill -9 #批量杀进程


