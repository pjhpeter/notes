el-form隐藏域处理
```
<el-form-item prop="id" hidden><!-- 隐藏域一定要在el-form-item加上hidden属性，不然空白div会占位置-->
    <el-input type="hidden" v-model="member.id"></el-input>
</el-form-item>
```
el-form的model需要初始化，避免不能输入的问题
```
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
element组件要绑定原生事件，需要在事件名后添加.native修饰符
```
<el-input v-model="searchMap.name" placeholder="供应商名称" clearable @keyup.enter.native="fetchData"></el-input>
```
element修改表头样式，添加header-cell-class-name
```
<el-table :data="list" border stripe height="480" header-cell-class-name="el-table-header">
```
全局css文件override-elment-ui.css
```
.el-table-header {
    background-color: #66b1ff !important;
    color: #fff;
}
```