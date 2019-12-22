### mavan打包项目是报找不到javax.servlet.Filter的类文件错误
原因是maven会到jre/lib/ext目录想找servlet-api.jar，所有只需要包jar包拷到那个目录下就行