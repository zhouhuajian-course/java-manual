# java manual

1. 在家目录 创建 .m2 目录，增加 settings.xml，使用国内源，并设置仓库位置为 D:\maven\.m2\repository
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">    
      <localRepository>D:\maven\.m2\repository</localRepository>
      <mirrors>
        <mirror>
          <id>alimaven</id>
          <mirrorOf>central</mirrorOf>
          <name>alimaven</name>
          <url>https://maven.aliyun.com/repository/public</url>
        </mirror>
      </mirrors>
    </settings>
    ```
