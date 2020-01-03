### 解决git did not exit cleanly (exit code 128)
#### 一、替换路径
1、鼠标右键 -> TortoiseGit -> Settings -> Network
2、SSH client was pointing to C:\Program Files\TortoiseGit\bin\TortoisePlink.exe
3、Changed path to C:\Program Files (x86)\Git\bin\ssh.exe
#### 二、使用HTTP格式的url，不要使用SSH格式的url
### git同步远程仓库错误fatal: refusing to merge unrelated histories
原因是本地仓库和远程仓库本来是两个独立的仓库，如果用git clone命令克隆的项目就不会有这样的问题
解决方法：
```cmd
git pull origin master --allow-unrelated-histories
```


