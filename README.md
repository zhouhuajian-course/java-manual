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
10. Spring 是一个生态体系或技术体系，但一般大家提 Spring 可能是指 Spring Framework，因为这是整个 Spring 生态的基石。其他 Spring Boot、Spring Data、Spring Security 等，都是基于这个 Spring Framework 开发起来的框架
11. Spring Boot 热部署 IDEA
```text
1. pom.xml 加依赖
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
  <scope>runtime</scope>
  <optional>true</optional>
</dependency>
2. Compiler 勾选 Build project automatically （没运行、没调试才生效）
3. Advanced Settings 勾选 Allow auto-make start even if developed application is currently running （这样第2步，运行中的也会生效）
默认好像延迟比较大，但这样不会消耗太多机器资源 Ctrl+Alt+Shift+/ 的 Register 应该可以把延迟调小   
```
12. （暂未看到其他项目这样用）Spring Boot 很多命名太长太繁琐，建议不是核心的单词都用缩写，例如 `WebApplication` -> `WebApp`，`UserController` -> `UserCtl`，`UserService` -> `UserSrv`，包名也是 `controller` -> `ctl` 这样更美观，把重要的信息突显，不重要的信息不突显，impl 就是个例子，多用3个或4个字母的缩写，不是重要的信息
13. mvn 命令 `goal(s)` `phase(s)` 省略了其他选项，需要时补上，很多选项，需要在有 pom.xml 的目录里执行
```cmd
> mvn -h

usage: mvn [options] [<goal(s)>] [<phase(s)>]     

Options:   省略其他选项，需要时，补上

 -D,--define <arg>                       Define a user property                  定义 pom.xml 的用户属性 注意后面有个空格 按照这文档 加上空格更规范
 -e,--errors                             Produce execution error messages
 -h,--help                               Display help information                显示帮助信息
 -q,--quiet                              Quiet output - only show errors         安静输出 只输出错误信息
 -v,--version                            Display version information             显示版本信息
 -V,--show-version                       Display version information             显示版本信息 不停止构建项目
                                         WITHOUT stopping build
```
14. `exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install --help"`，到代码中 args 会成为 main 方法的 args，也就是 `args 是字符串数组 ["install", "--help"]`
15. Spring Boot `@RestController` 不一定要写 RESTful 接口，写普通接口也可以，`@Controller` 尽量返回的就是模板，严格按照 `MVC` 模式，`Service` 如果业务简单，不需要一定要 使用 接口和 impl 的方式，需要多种实现方式时，才用这种设计方式，例如 翻译接口，要翻译成 英语、法语、德语等，一个接口，多个实现，其他尽量别用接口、实现的方式，会让项目更臃肿
16. Spring Boot `Jar` 包打包方式的推荐的方式，内嵌 Servlet 容器，例如 Tomcat，`War` 包打包方式不太推荐，是比较传统的打包方式
17. Spring Boot `@PathVariable` 注解
```java
  @RequestMapping("/user/{id}")
  public String userInfo(@PathVariable int id) { // 参数名和URL变量名一样
    System.out.println(id);
    // ...
  }

  @GetMapping("/friends/{id}")
  public String getFriends(@PathVariable("id") int userId) {  // 参数名和URL变量名不一样
    System.out.println(userId);
    // ...
  }
```
18. 判断是否是 Windows 系统 `System.getProperty("os.name").toLowerCase().contains("windows")`
