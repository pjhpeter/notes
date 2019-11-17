在github上将vue-devtools克隆下来，目录自己随便定
```
cd d:\git
git clone https://github.com/vuejs/vue-devtools.git
```
到vue-devtools目录下，安装依赖，前提是电脑已经安装好nodejs6.x以上版本，这里要等很久，耐心点
```
cd d:\git\vue-devtools
npm install
```
找到\vue-devtools\packages\shell-chrome\manifest.json，修改下面参数 
```
"persistent": true// 原来是false
```
回到命令行执行命令安装webpack
```
npm install -D webpack
npm install -D webpack-cli
```
编译vue-devtools
```
npm run build
```