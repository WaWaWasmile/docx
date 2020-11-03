项目从GitHub上下载下来pom文件报错：

maven构建错误Cannot resolve plugin org.apache.maven.plugins:maven-clean-plugin:3.1.0

在pom文件的\<project\>下添加

```pr
<repositories>
    <repository>
        <id>alimaven</id>
        <url>https://maven.aliyun.com/repository/public</url>
    </repository>
</repositories>
<pluginRepositories>
     <pluginRepository>
         <id>alimaven</id>
         <url>https://maven.aliyun.com/repository/public</url>
     </pluginRepository>
</pluginRepositories>
```

