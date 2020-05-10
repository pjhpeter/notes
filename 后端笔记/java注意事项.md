### mavan打包项目是报找不到javax.servlet.Filter的类文件错误
原因是maven会到jre/lib/ext目录想找servlet-api.jar，所有只需要包jar包拷到那个目录下就行

### JPA查询懒加载报no session错误
在service添加@Transactional，只有查询逻辑最好加上readonly = true

### Spring Cache注解有时候不起作用
Spring的缓存注解只能public类型的方法上

### 查看jit汇编信息JVM配置
```cmd
-server -XX:+PrintCompilation -XX:+UnlockDiagnosticVMOptions -XX:+PrintAssembly -XX:+LogCompilation -XX:LogFile=jit.log
```

### Win10查看jit汇编信息报错
- 错误

Could not load hsdis-amd64.dll; library not loadable; PrintAssembly is disabled

- 解决

下载hsdis

http://vorboss.dl.sourceforge.net/project/fcml/fcml-1.1.1/hsdis-1.1.1-win32-amd64.zip

下载对应版本解压得到dll，保存到jre\bin\server就可以了

### 查看JVM的GC日志的JVM配置
```cmd
-server -verbose:gc -XX:+PrintGCDetails
```

### 查询list时，必须限制大小
防止前端传来的参数没有严格校验导致全表查询，形成数据来太大的list，造成内存溢出错误