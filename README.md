# java manual

1. Maven尽量使用已安装，而不是IDEA自带，https://maven.apache.org/ ，安装到D盘，改conf/settings.xml，mirrors下增加，增加本地仓库配置，默认${user.home}/.m2/repository
   ```
   <mirror>
      <id>alimaven</id>
      <mirrorOf>central</mirrorOf>
      <name>alimaven</name>
      <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
   ```

   ```
   <localRepository>D:\maven\repo</localRepository>
   ```
