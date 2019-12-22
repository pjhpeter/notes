### 安装JDK
没什么好讲的
### 安装插件
1.Language Support for Java(TM) by Red Hat
2.Maven for Java
3.Lombok Annotations Support for VS Code，自动生成getter和setter
4.如果要用Spring Boot就安装Spring Boot Extension Pack
5.习惯用eclipse快捷键的可以装Eclipse Keymap
### vscode配置
1.系统环境变量一定要配
2.配置vscode的settings.json，最后
```
{
    "java.configuration.maven.userSettings": "D:/work/apache-maven-3.6.3/conf/settings.xml",
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/target": true,
        "**/logs": true
    },
    "workbench.editor.enablePreview": false
}
```