+ el-form隐藏域处理
```vue
<el-form-item prop="id" hidden><!-- 隐藏域一定要在el-form-item加上hidden属性，不然空白div会占位置-->
    <el-input type="hidden" v-model="member.id"></el-input>
</el-form-item>
```
+ el-form的model需要初始化，避免不能输入的问题
```json
member: {// 初始化各字段，数字用null，避免不能输入的问题
    id: null,
    name: "",
    cardNo: "",
    birthday: null,
    phone: "",
    money: null,
    integral: null,
    payType: null,
    address: ""
}
```
+ element组件要绑定原生事件，需要在事件名后添加.native修饰符
```vue
<el-input v-model="searchMap.name" placeholder="供应商名称" clearable @keyup.enter.native="fetchData"></el-input>
```
+ element修改表头样式，添加header-cell-class-name
```vue
<el-table :data="list" border stripe height="480" header-cell-class-name="el-table-header">
```
+ 全局css文件override-elment-ui.css
```css
.el-table-header {
    background-color: #66b1ff !important;
    color: #fff;
}
```
+ Vue动态加载路由时，会出现刷新页面变成空白页的情况，是由于刷新时路由跳转，但组件没有异步加载完成，所以找不到对应组件和路由，解决方法如下：
```js
// 刷新页面标志
let doRefresh = true;
async function doNext(to, next) {
  // 解决刷新页面
  if (doRefresh) {
    doRefresh = false;
    store.dispatch("SetRouter", router);
    // 发请求获取菜单数据
    await store.dispatch("SetMenuTree");
    // 强制指定路由跳转的组件，并不留历史痕迹
    next({ ...to, replace: true });
  }
  next();
}
```
Vue-cli4配置sass全局变量

[转载的](https://blog.csdn.net/qq_41595903/article/details/103381055)

Vue+ViewUI时，enlint报Parsing error: x-invalid-end-tag错误
1. 在vscode的setting.json中添加：
```json
"vetur.validation.template": false
```
2. 在.eslintrc.js的rules中添加：
```js
"vue/no-parsing-error": [2, { "x-invalid-end-tag": false }]
```
3. 重启vscode

+ ViewUi的Modal组件的fullscreen和draggable不能共用