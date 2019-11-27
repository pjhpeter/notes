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