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
12. 经管名称长，无所谓，可以多写名称长的命名，但不建议 fs 这种缩写（暂未看到其他项目这样用）~~Spring Boot 很多命名太长太繁琐，建议不是核心的单词都用缩写，例如 `WebApplication` -> `WebApp`，`UserController` -> `UserCtl`，`UserService` -> `UserSrv`，包名也是 `controller` -> `ctl` 这样更美观，把重要的信息突显，不重要的信息不突显，impl 就是个例子，多用3个或4个字母的缩写，不是重要的信息~~
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
19. 创建临时目录 `java.nio.file.Files#createTempDirectory(java.lang.String, java.nio.file.attribute.FileAttribute<?>...)`
```
// C:\Users\ZHOUHU~1\AppData\Local\Temp\7523101765255010963 
// C:\Users\ZHOUHU~1\AppData\Local\Temp\playwright-java-7523101765255010963 提供前缀
```
20. Spring Boot 控制器 类和方法 定义 都加 public。先写类，再写注解；先写方法，再写注解；先写参数，再写注解。
21. `Arrays`数组工具类，`Arrays.asList()` 可以方便把数组转成列表，数组修改，列表也会跟着修改，列表修改，数组也会跟着修改，但是不允许做修改 size 的操作，会抛 `UnsupportedOperationException`；另外这方法，还可提供多个元素，方便的生成 fixed-size 的列表，不是使用数组，而是一次性提供多个元素。当不需要添加或删除元素时，使用这个`Arrays.asList()`比较方便；当需要添加或删除元素时，使用`new java.util.ArrayList()`，一个一个添加元素。
    用`Arrays.toString()`可以方便打印数组。
```java
import java.util.Arrays;
import java.util.List;

public class Test {
  
public class Test {
  public static void main(String[] args) {
    // 1. 把数组转成固定大小的列表
    String[] names = {"Lily", "Tom", "Lucy"};
    List<String> nameList = Arrays.asList(names);

    // System.out.println(names[0] + " " + names[1] + " " + names[2]);
    System.out.println(Arrays.toString(names));
    System.out.println(nameList);

    names[0] = "Joe";
    nameList.set(1, "Trump");

    // System.out.println(names[0] + " " + names[1] + " " + names[2]);
    System.out.println(Arrays.toString(names));
    System.out.println(nameList);
    
    // 2. 提供多个元素 创建 固定大小的列表
    List<String> friends = Arrays.asList("Harris", "Tina", "Mike");
    // UnsupportedOperationException
    // friends.add("Tim");
    System.out.println();
    System.out.println(friends);
  }
}
}
/*
[Lily, Tom, Lucy]
[Lily, Tom, Lucy]
[Joe, Trump, Lucy]
[Joe, Trump, Lucy]

[Harris, Tina, Mike]
*/
```
22. Spring Boot 重定向 `redirect:/...` `redirect:http://...` `https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/viewresolver.html#mvc-redirecting-redirect-prefix`
23. 遍历一般用`for-each loop` `for-each 循环` 或者叫 `Enhanced For` 增强的for循环，需要索2引时，用`for loop` `for statement` `for 循环`，`https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html` `https://docs.oracle.com/javase/8/docs/technotes/guides/language/foreach.html`
24. `try-with-resources statement 语句` 是一种 `try statement 语句`，`https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html` `The try-with-resources statement is a try statement that declares one or more resources. A resource is an object that must be closed after the program is finished with it. The try-with-resources statement ensures that each resource is closed at the end of the statement. Any object that implements java.lang.AutoCloseable, which includes all objects which implement java.io.Closeable, can be used as a resource.` 
25. Spring Boot 获取 Cookie，也可使用`@CookieValue`注解获取，推荐使用注解，而不是HttpServletRequest的方式获取
```java
package web.controller;

import jakarta.servlet.http.Cookie;
import jakarta.servlet.http.HttpServletRequest;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;

@RestController
public class TestController {
  @GetMapping("/test")
  public String test(HttpServletRequest request)
  {
    Cookie[] cookies = request.getCookies();
    for (Cookie cookie : cookies) {
      System.out.println(cookie.getName());
      System.out.println(cookie.getValue());
    }
    return Arrays.toString(cookies);
  }
}
```
26. Spring Boot 获取表单数据，推荐使用注解、参数注入的方式，而不是 HttpServletRequest，当然可以的话，封装成对象的方式，也是推荐的
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>个人资料</title>
</head>
<body>
  <form action="/profile" method="post" enctype="multipart/form-data">
    <div>姓名：<input type="text" name="name" /></div>
    <div>性别：<input type="radio" name="gender" value="男" />男
              <input type="radio" name="gender" value="女" />女
    </div>
    <div>语言：<input type="checkbox" name="languages" value="汉语" />汉语
              <input type="checkbox" name="languages" value="英语" />英语
    </div>
    <div>生日：<input type="date" name="birthday" /></div>
    <div>颜色：<input type="color" name="color" /></div>
    <div>范围：<input type="range" name="range" min="0" value="0" max="100" /></div>
    <div>头像：<input type="file" name="avatar" /></div>
    <div>学校：<select name="school">
                <option value="">请选择</option>
                <option value="小学">小学</option>
                <option value="初中">初中</option>
                <option value="高中">高中</option>
              </select>
    </div>
    <div>简介：<textarea name="intro"></textarea></div>
    <div>照片：<input type="file" name="photos" multiple /></div>
    <div><button type="submit">保存</button></div>
  </form>
</body>
</html>
```
```java
package web.controller;

import jakarta.servlet.http.HttpServletRequest;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;
import org.springframework.web.multipart.MultipartHttpServletRequest;
import org.springframework.web.multipart.MultipartRequest;

import java.io.IOException;
import java.nio.file.Path;
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.Set;

@Controller
public class ProfileController {

  @GetMapping("/profile")
  public String profile() {
    return "profile";
  }

  @PostMapping("/profile")
  public String profile(
    @RequestParam String name,
    @RequestParam String gender,
    @RequestParam String[] languages,
    @RequestParam String birthday,
    @RequestParam String color,
    @RequestParam String range,
    @RequestParam MultipartFile avatar,
    @RequestParam String school,
    @RequestParam String intro,
    @RequestParam MultipartFile[] photos
  ) throws IOException {
    System.out.println("姓名：" + name);
    System.out.println("性别：" + gender);
    System.out.println("语言：" + Arrays.toString(languages));
    System.out.println("生日：" + birthday);
    System.out.println("颜色：" + color);
    System.out.println("范围：" + range);
    System.out.println("头像：" + avatar.getOriginalFilename() + " " + avatar.getSize());
    System.out.println("学校：" + school);
    System.out.println("简介：" + intro);
    System.out.println("图片：");
    for (MultipartFile photo : photos) {
      System.out.println("      " + photo.getOriginalFilename() + " " + photo.getSize());
    }
    // avatar.transferTo(Path.of("learn/avatar.svg"));
    return "redirect:/profile";
  }

  @PostMapping("/profile2")
  public String profile(HttpServletRequest req)
  {
    MultipartHttpServletRequest request = (MultipartHttpServletRequest) req;
    System.out.println("姓名：" + request.getParameter("name"));
    System.out.println("性别：" + request.getParameter("gender"));
    System.out.println("语言：" + Arrays.toString(request.getParameterValues("languages")));
    System.out.println("生日：" + request.getParameter("birthday"));
    System.out.println("颜色：" + request.getParameter("color"));
    System.out.println("范围：" + request.getParameter("range"));
    System.out.println("头像：" + request.getFile("avatar").getOriginalFilename() + " " + request.getFile("avatar").getSize());
    System.out.println("学校：" + request.getParameter("school"));
    System.out.println("简介：" + request.getParameter("intro"));
    System.out.println("照片：");
    List<MultipartFile> photos = request.getFiles("photos");
    for (MultipartFile photo : photos) {
      System.out.println("      " + photo.getOriginalFilename() + " " + photo.getSize());
    }
    return "redirect:/profile";
  }
}
```
27. Maven 项目使用 JUnit 5
```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>5.11.1</version>
  <scope>test</scope>
</dependency>
```
