### mavan打包项目是报找不到javax.servlet.Filter的类文件错误
原因是maven会到jre/lib/ext目录想找servlet-api.jar，所有只需要包jar包拷到那个目录下就行

### JPA查询懒加载报no session错误
在service添加@Transactional，只有查询逻辑最好加上readonly = true

### Spring Cache注解有时候不起作用
Spring的缓存注解只能public类型的方法上