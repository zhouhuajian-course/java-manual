# java manual

1. 在家目录 创建 .m2 目录，增加 settings.xml，使用国内源，并设置仓库位置为 D:\maven\.m2\repository，IDEA会默认使用该 settings.xml，Build Tools -> Maven 里面，另外 settings.xml 如果一开始没有，可以下载 maven，拷贝conf目录里面的settings.xml，很重要，避免仓库默认在C盘，还有避免每个用户家目录.m2都有个repository仓库，家目录的.m2/repository 可以删掉
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
2. Java 代码比较多，可以考虑 像html,css,js 一样使用两个空格的缩进，让代码更美观，开源库 playwright-java 就是两个空格的缩进
3. 创建一个 Spring Boot 项目。在 `https://start.spring.io/` 创建一个 Web 项目，依赖搜索 Web，选择 `Spring Web` 依赖 `Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.` `https://spring.io/quickstart`。静态资源 `Static resources, including HTML and JavaScript and CSS`，直接放 `resources/static` 目录，或 `resources/public`。 `index.html` 比较特殊，会被当做 `a "welcome page"` `http://localhost:8080/`，貌似不需要 `Spring Boot DevTools`，只需 `Spring Web` 即可
4. 由于启动前需要编译的原因，而且是编译都指定的另一个目录，所以 `Spring Boot` 静态资源 `resources/static` 有改动，需要重启应用才能生效，增删改都一样，可以用  `Spring Boot DevTools` 优化，但默认如此
5. 创建一个 使用模板引擎的 Spring Boot 项目， `https://start.spring.io/` 添加 `Spring Web` `Thymeleaf` (Spring Boot 官方推荐的模板引擎 /taɪm li:f/) `Spring Boot DevTools` (主要用来热部署，发现代码有改动，自动重启应用 
`Provides fast application restarts, LiveReload, and configurations for enhanced development experience.`) `https://spring.io/guides/gs/serving-web-content`
6. IDEA maven 包 没有文档的问题 -> 打开 Maven 面板，点击 下载 -> 点击 下载 文档 即可
7. Maven 项目 包名不知道怎么写，可以写成项目名 例如 项目名是 web ，那么包名也叫 web
8. Spring Boot 修改服务器端口 `application.properties` `server.port=80`
9. 获取环境变量 `System.getenv("JAVA_HOME")`
10. 
