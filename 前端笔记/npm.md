### 版本管理
```cmd
假设初始版本为0.1.0
➜  xxx git:(master) npm version preminor
v0.1.0-0
➜  xxx git:(master) npm version minor
v0.1.0
➜  xxx git:(master) npm version prepatch
v0.1.1-0
➜  xxx git:(master) npm version patch   
v0.1.1
➜  xxx git:(master) npm version prerelease
v0.1.2-0
➜  xxx git:(master) npm version premajor
v1.0.0-0
➜  xxx git:(master) npm version major   
v1.0.0
```
### NPM设置淘宝镜像
1.查询当前配置的镜像
```
npm get registry 
> https://registry.npmjs.org/
```
设置成淘宝镜像
```
npm config set registry http://registry.npm.taobao.org/
```
2.换成原来的
```
npm config set registry https://registry.npmjs.org/
```

### Yarn 设置淘宝镜像
1.查询当前配置的镜像
```
yarn config get registry
> https://registry.yarnpkg.com
```
设置成淘宝镜像
```
yarn config set registry http://registry.npm.taobao.org/
```
### 安装完Yarn后必须配置环境变量
将下面的路径添加到path中，不然通过Yarn安装的组件会出现找不到命令的问题
```
-- 命令行中输入查看Yarn的全局路径命令
yarn global dir
> /home/user/.local/yarn/global

-- 将返回的路径下面的/node_modules/.bin添加到path环境变量中,比如这个：
/home/user/.local/yarn/global/node_modules/.bin
```
### yarn更新依赖
```cmd
yarn upgrade-interactive
```