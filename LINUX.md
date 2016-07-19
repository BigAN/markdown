# linux

## 问题

怎么通过端口号来找到程序？

> - find the process (PID) listening on port 3200 (check it in settings>scala>tcp port)    
>   - on Mac(Linux): `lsof -i :3200`
>
> - check that process
>   - on Mac(Linux): `ps axu |grep `
>   - in my case it ended with `org.jetbrains.plugins.scala.nailgun.NailgunRunner 3200`
> - kill the process, it is some old one and IDEA will start the new one
>   - on Mac(Linux): `kill -9 `



## awk