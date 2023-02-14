windows技巧
1、手动锁Bitlocker
运行cmd或powershell（需管理员权限），执行命令
manage-bde.exe F: -lock
2、一行cmd代码查询所有连过的wifi密码
需要管理员权限运行cmd

for/f "skip=10 tokens=1,2 delims=:"%i in ('netsh wlan show profiles') do@for/f "tokens=1-2delims=:"%k in ('netsh wlan show profiles %j key ^=clear ^|findstr /i "关键内容"') do@echo %j,%l>>%USERPROFILE%\desktop\wifi.txt


