
**==第一部分==**

[toc]
# 一、初始Spring Boot
## 1.1 Spring Boot 简介
Spring官网首页对Spring Boot的介绍

Spring Boot

BUILD ANYTHING

Spring Boot is designed to get you up and running as quickly as possible, 
with minimal upfront configuration of Spring. 
Spring Boot takes an opinionated view of building production-ready applications.

Spring Boot 为快速启动且最小化配置的Spring应用而设计。
Spring Boot 具有一套固化的视图，该视图用于构建生产级别的应用。
这些应用具备了开发（Dev）和运维（Ops）的能力，即业界常提及的DevOps。


Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".

Spring Boot 使得构建独立的，生产级别的Spring应用变得简单。



We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration

使用Spring平台和第三方库的固化视图，我们可以最简单的使用它们。大部分的Spring Boot应用只需要极少的Spring配置。

## 1.2 SpringBoot 特性（Features）
- Create stand-alone Spring applications
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
- Provide opinionated 'starter' dependencies to simplify your build configuration
- Automatically configure Spring and 3rd party libraries whenever possible
- Provide production-ready features such as metrics, health checks and externalized configuration
- Absolutely no code generation and no requirement for XML configuration

中文含义如下：

- 创建独立的Spring应用
- 直接嵌入Tomcat、Jetty或Undertow等Web容器（不需要部署WAR文件）
- 提供固化的“starter”依赖，简化构建配置
- 当条件满足时自动地装配Spring或第三方类库
- 提供运维（Production-Ready）特性，如指标信息、健康检查及外部化配置；
- 绝无代码生成，并且不需要XML配置

# 二、独立的Spring应用
1. 为什么是独立的应用？

Spring Boot 应用无须再像传统的Java EE 应用那样，将应用打包成WAR文件或EAR文件，并部署到Java EE容器中运行。Spring Boot应用采用嵌入式容器，独立于外部容器，对应用生命周期拥有完全自主的控制，从此改变了“寄人篱下”的境地。

2. 为什么是Spring应用，而不是Spring Boot应用


3. 创建Spring Boot应用的方法有两个：

- 命令行创建方式
- 图形创建方式

4. 运行Spring Boot方式有两种

- 生产环境运行方式
- 开发阶段运行方式

## 2.1 创建 Spring Boot 应用

### 2.1.1 命令行方式创建Spring Boot应用

1. 使用 Maven Archetype 插件，生成基本的项目结构
```cmd
mvn archetype:generate -DgroupId=thingking-in-spring-boot -DartifactId=first-spring-boot-application -Dversion=1.0.0-SNAPSHOT -DinteractiveMode=false -Dpackage=thinking.in.spring.boot -s D:\javaenv\apache-maven-3.3.1\conf\settings-common.xml
```

执行结果如下：

```
1.0/maven-archetype-quickstart-1.0.jar
Downloaded: http://maven.aliyun.com/nexus/content/groups/public/org/apache/maven/archetypes/maven-archetype-quickstart/1.0/maven-archetype-quickstart-1.0.jar (5 KB at 9.4 KB/sec)
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-quickstart:1.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: basedir, Value: E:\demo
[INFO] Parameter: package, Value: thinking.in.spring.boot
[INFO] Parameter: groupId, Value: thingking-in-spring-boot
[INFO] Parameter: artifactId, Value: first-spring-boot-application
[INFO] Parameter: packageName, Value: thinking.in.spring.boot
[INFO] Parameter: version, Value: 1.0.0-SNAPSHOT
[INFO] project created from Old (1.x) Archetype in dir: E:\demo\first-spring-boot-application
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 8.653 s
[INFO] Finished at: 2020-01-26T23:43:02+08:00
[INFO] Final Memory: 17M/171M
[INFO] ------------------------------------------------------------------------
```

执行后的目录结构为：
```
E:\demo\first-spring-boot-application>tree
卷 本地磁盘 的文件夹 PATH 列表
卷序列号为 9A71-0EA9
E:.
└─src
    ├─main
    │  └─java
    │      └─thinking
    │          └─in
    │              └─spring
    │                  └─boot
    └─test
        └─java
            └─thinking
                └─in
                    └─spring
                        └─boot

E:\demo\first-spring-boot-application>
```
2. 为生成的pom文件，添加Spring Boot相关依赖

原pom.xml内容为：
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>thingking-in-spring-boot</groupId>
  <artifactId>first-spring-boot-application</artifactId>
  <packaging>jar</packaging>
  <version>1.0.0-SNAPSHOT</version>
  <name>first-spring-boot-application</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

3. 为生成的pom文件，添加Spring Boot相关依赖

添加spring-boot-starter-web依赖
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>thingking-in-spring-boot</groupId>
  <artifactId>first-spring-boot-application</artifactId>
  <packaging>jar</packaging>
  <version>1.0.0-SNAPSHOT</version>
  <name>《Spring Boot 编程思想》第一个spring boot 应用</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <!-- 增加spring boot web依赖 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
      <version>2.0.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

执行 mvn dependency:tree -Dincludes=org.springframework*，观察项目依赖树的变化

```
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building ??Spring Boot ???????????spring boot ??? 1.0.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ first-spring-boot-application ---
[INFO] thingking-in-spring-boot:first-spring-boot-application:jar:1.0.0-SNAPSHOT
[INFO] +- org.springframework.boot:spring-boot-starter-web:jar:2.0.2.RELEASE:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter:jar:2.0.2.RELEASE:compile
[INFO] |  |  +- org.springframework.boot:spring-boot:jar:2.0.2.RELEASE:compile
[INFO] |  |  +- org.springframework.boot:spring-boot-autoconfigure:jar:2.0.2.RELEASE:compile
[INFO] |  |  +- org.springframework.boot:spring-boot-starter-logging:jar:2.0.2.RELEASE:compile
[INFO] |  |  |  +- ch.qos.logback:logback-classic:jar:1.2.3:compile
[INFO] |  |  |  |  +- ch.qos.logback:logback-core:jar:1.2.3:compile
[INFO] |  |  |  |  \- org.slf4j:slf4j-api:jar:1.7.25:compile
[INFO] |  |  |  +- org.apache.logging.log4j:log4j-to-slf4j:jar:2.10.0:compile
[INFO] |  |  |  |  \- org.apache.logging.log4j:log4j-api:jar:2.10.0:compile
[INFO] |  |  |  \- org.slf4j:jul-to-slf4j:jar:1.7.25:compile
[INFO] |  |  +- javax.annotation:javax.annotation-api:jar:1.3.2:compile
[INFO] |  |  +- org.springframework:spring-core:jar:5.0.6.RELEASE:compile
[INFO] |  |  |  \- org.springframework:spring-jcl:jar:5.0.6.RELEASE:compile
[INFO] |  |  \- org.yaml:snakeyaml:jar:1.19:runtime
[INFO] |  +- org.springframework.boot:spring-boot-starter-json:jar:2.0.2.RELEASE:compile
[INFO] |  |  +- com.fasterxml.jackson.core:jackson-databind:jar:2.9.5:compile
[INFO] |  |  |  +- com.fasterxml.jackson.core:jackson-annotations:jar:2.9.0:compile
[INFO] |  |  |  \- com.fasterxml.jackson.core:jackson-core:jar:2.9.5:compile
[INFO] |  |  +- com.fasterxml.jackson.datatype:jackson-datatype-jdk8:jar:2.9.5:compile
[INFO] |  |  +- com.fasterxml.jackson.datatype:jackson-datatype-jsr310:jar:2.9.5:compile
[INFO] |  |  \- com.fasterxml.jackson.module:jackson-module-parameter-names:jar:2.9.5:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter-tomcat:jar:2.0.2.RELEASE:compile
[INFO] |  |  +- org.apache.tomcat.embed:tomcat-embed-core:jar:8.5.31:compile
[INFO] |  |  +- org.apache.tomcat.embed:tomcat-embed-el:jar:8.5.31:compile
[INFO] |  |  \- org.apache.tomcat.embed:tomcat-embed-websocket:jar:8.5.31:compile
[INFO] |  +- org.hibernate.validator:hibernate-validator:jar:6.0.9.Final:compile
[INFO] |  |  +- javax.validation:validation-api:jar:2.0.1.Final:compile
[INFO] |  |  +- org.jboss.logging:jboss-logging:jar:3.3.2.Final:compile
[INFO] |  |  \- com.fasterxml:classmate:jar:1.3.4:compile
[INFO] |  +- org.springframework:spring-web:jar:5.0.6.RELEASE:compile
[INFO] |  |  \- org.springframework:spring-beans:jar:5.0.6.RELEASE:compile
[INFO] |  \- org.springframework:spring-webmvc:jar:5.0.6.RELEASE:compile
[INFO] |     +- org.springframework:spring-aop:jar:5.0.6.RELEASE:compile
[INFO] |     +- org.springframework:spring-context:jar:5.0.6.RELEASE:compile
[INFO] |     \- org.springframework:spring-expression:jar:5.0.6.RELEASE:compile
[INFO] \- junit:junit:jar:3.8.1:test
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.408 s
[INFO] Finished at: 2020-01-26T23:54:20+08:00
[INFO] Final Memory: 16M/222M
[INFO] ------------------------------------------------------------------------
```
其中 spring-webmvc和tomcat等依赖已经被依赖进来了。

说明了spring boot 第三点的特性：

"provide opinionated 'starter' dependencies to simplify your build configuration".


4. 增加执行代码
- thinking.in.spring.boot.App源码如下：
```java
package thinking.in.spring.boot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

/**
 * Hello world!
 *
 */
@RestController
@SpringBootApplication
public class App {

	@RequestMapping("/")
	public String index() {
		return "Hello, World";
	}
	
    public static void main( String[] args ) {
        SpringApplication.run(App.class, args);
    }
}

```
直接运行结果如下：
```
E:\demo\first-spring-boot-application>mvn spring-boot:run
[INFO] Scanning for projects...
Downloading: https://repo.maven.apache.org/maven2/org/codehaus/mojo/maven-metadata.xml
Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-metadata.xml
Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-metadata.xml (14 KB at 1.8 KB/sec)
Downloaded: https://repo.maven.apache.org/maven2/org/codehaus/mojo/maven-metadata.xml (20 KB at 1.5 KB/sec)
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 14.493 s
[INFO] Finished at: 2020-01-27T00:02:53+08:00
[INFO] Final Memory: 9M/153M
[INFO] ------------------------------------------------------------------------
[ERROR] No plugin found for prefix 'spring-boot' in the current project and in the plugin groups [org.apache.maven.plugins, org.codehaus.mojo] available from the repositories [local (D:\javaenv\mvnrepository), central (https://repo.maven.apache.org/maven2)] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/NoPluginFoundForPrefixException
```
5. 使用Spring Boot Maven插件引导Spring Boot 应用
在pom.xml文件中添加spring-boot-starter-parent 信息
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

  	<!-- 添加 Spring Boot Parent POM -->
    <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.2.RELEASE</version>
    </parent>
    
  <modelVersion>4.0.0</modelVersion>
  <groupId>thingking-in-spring-boot</groupId>
  <artifactId>first-spring-boot-application</artifactId>
  <packaging>jar</packaging>
  <version>1.0.0-SNAPSHOT</version>
  <name>《Spring Boot 编程思想》第一个spring boot 应用</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <!-- 增加spring boot web依赖 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>

```

6. 再次执行相关命令
```cmd
mvn spring-boot:run -s D:\javaenv\apache-maven-3.3.1\conf\settings-common.xml
```

运行结果为：
```
: org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@49ace22c: startup date [Mon Jan 27 00:07:27 CST 2020]; root of context hierarchy
2020-01-27 00:07:29.724  INFO 15052 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/]}" onto public java.lang.String thinking.in.spring.boot.App.index()
2020-01-27 00:07:29.731  INFO 15052 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error]}" onto public org.springframework.http.ResponseEntity<java.util.Map<java.lang.String, java.lang.Object>> org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.error(javax.servlet.http.HttpServletRequest)
2020-01-27 00:07:29.732  INFO 15052 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error],produces=[text/html]}" onto public org.springframework.web.servlet.ModelAndView org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.errorHtml(javax.servlet.http.HttpServletRequest,javax.servlet.http.HttpServletResponse)
2020-01-27 00:07:29.758  INFO 15052 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/webjars/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2020-01-27 00:07:29.759  INFO 15052 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2020-01-27 00:07:29.930  INFO 15052 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
2020-01-27 00:07:30.009  INFO 15052 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-01-27 00:07:30.024  INFO 15052 --- [           main] thinking.in.spring.boot.App              : Started App in 3.191 seconds (JVM running for 15.707)
```

7. 检验Spring Boot 应用HTTP服务

浏览器访问 http://localhost:8080/

返回结果：Hello, World
```
C:\Users\Legend>curl http://localhost:8080/
Hello, World
C:\Users\Legend>
```

### 2.1.2 图形化界面创建 Spring Boot 应用
直接访问网址：[Spring Initializr](https://start.spring.io/)：https://start.spring.io/ ，在页面表单中进行相应配置，直接生成基础的脚手架。生成的压缩文件解压后的结构如下：
```
E:\demo\first-app-by-gui>tree /F
卷 本地磁盘 的文件夹 PATH 列表
卷序列号为 9A71-0EA9
E:.
│  .gitignore
│  HELP.md
│  mvnw
│  mvnw.cmd
│  pom.xml
│
├─.mvn
│  └─wrapper
│          maven-wrapper.jar
│          maven-wrapper.properties
│          MavenWrapperDownloader.java
│
└─src
    ├─main
    │  ├─java
    │  │  └─thinkinginspringboot
    │  │      └─firstappbygui
    │  │              FirstAppByGuiApplication.java
    │  │
    │  └─resources
    │      │  application.properties
    │      │
    │      ├─static
    │      └─templates
    └─test
        └─java
            └─thinkinginspringboot
                └─firstappbygui
                        FirstAppByGuiApplicationTests.java
```
1. Spring Boot 模板应用目录结构

（1）.gitignore

git的忽略文件列表配置，在该文件中配置的文件或路径将被git版本管理忽略。

（2）Maven Wrapper文件

参见项目：[Maven Wrapper](https://github.com/takari/maven-wrapper)：https://github.com/takari/maven-wrapper
- .mvn/wrapper/maven-wrapper.jar

该文件由脚本引导，用于从Maven官方下载Maven二进制文件

- .mvn/wrapper/maven-wrapper.properties

此Properties文件定义了文件下载的URL，当其URL不可用时，由wrapperUrl属性配置

- mvnw 和 mvnw.cmd

两个文件具有相同的职责，引导 .mvn/wrapper/maven-wrapper.jar下载Maven二进制文件，前者用于*nix平台，后者工作于windows操作系统。

直接使用maven时的命令如下：```$mvn clean install```

使用Maven Wrapper时的命令为：```$mvnw clean install``` or on windows ```$mvnw.cmd clean install```

可以用mvnw或mvnw.cmd配置spring-boot:run插件使用

（3）Spring Boot 应用属性配置文件——application.properties

spring boot 默认的外部化配置文件

（4）Spring Boot 应用Junit测试文件

FirstAppByGuiApplicationTests.java为Spring Boot应用的模板JUnit测试文件
```java
package thinkinginspringboot.firstappbygui;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class FirstAppByGuiApplicationTests {

	@Test
	void contextLoads() {
	}

}

```
2. 使用mvnw.cmd脚本执行Spring Boot Maven插件
```cmd
mvnw.cmd spring-boot:run
```
即可启动Spring Boot应用。

```
E:\demo\first-app-by-gui>mvnw.cmd spring-boot:run

```

==**启动结果是无响应，不知道是不是仓库速度的影响！**==


### 2.1.3 创建 Spring Boot 应用可执行 JAR

首先要创建可执行JAR，必须添加spring-boot-maven-plugin插件到pom.xml中，而该插件默认会被追加到由https://start.spring.io构建的Spring Boot应用中。

```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	</plugins>
</build>
```

执行 mvn package
```
mvn package -s D:\javaenv\apache-maven-3.3.1\conf\settings-common.xml
```
执行结果如下：
```java
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.4.RELEASE)

2020-01-27 15:47:59.810  INFO 1108 --- [           main] t.f.FirstAppByGuiApplicationTests        : Starting FirstAppByGuiApplicationTests on DESKTOP-BJTPS78 with PID 1108 (started by Legend in E:\demo\first-app-by-gui)
2020-01-27 15:47:59.812  INFO 1108 --- [           main] t.f.FirstAppByGuiApplicationTests        : No active profile set, falling back to default profiles: default
2020-01-27 15:48:01.195  INFO 1108 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2020-01-27 15:48:01.477  INFO 1108 --- [           main] t.f.FirstAppByGuiApplicationTests        : Started FirstAppByGuiApplicationTests in 1.959 seconds (JVM running for 3.215)
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 2.771 s - in thinkinginspringboot.firstappbygui.FirstAppByGuiApplicationTests
2020-01-27 15:48:01.822  INFO 1108 --- [extShutdownHook] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- maven-jar-plugin:3.1.2:jar (default-jar) @ first-app-by-gui ---
[INFO] Building jar: E:\demo\first-app-by-gui\target\first-app-by-gui-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.2.4.RELEASE:repackage (repackage) @ first-app-by-gui ---
Downloading: http://maven.aliyun.com/nexus/content/groups/public/org/springframework/boot/spring-boot-loader-tools/2.2.4.RELEASE/spring-boot-loader-tools-2.2.4.RELEASE.pom
Downloaded: http://maven.aliyun.com/nexus/content/groups/public/org/springframework/boot/spring-boot-loader-tools/2.2.4.RELEASE/spring-boot-loader-tools-2.2.4.RELEASE.pom (3 KB at 6.2 KB/sec)
Downloading: http://maven.aliyun.com/nexus/content/groups/public/org/springframework/boot/spring-boot-loader-tools/2.2.4.RELEASE/spring-boot-loader-tools-2.2.4.RELEASE.jar
Downloaded: http://maven.aliyun.com/nexus/content/groups/public/org/springframework/boot/spring-boot-loader-tools/2.2.4.RELEASE/spring-boot-loader-tools-2.2.4.RELEASE.jar (151 KB at 312.4 KB/sec)
[INFO] Replacing main artifact with repackaged archive
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 27.321 s
[INFO] Finished at: 2020-01-27T15:48:05+08:00
[INFO] Final Memory: 40M/266M
[INFO] ------------------------------------------------------------------------
```
执行了一个单元测试并生成了一个可执行jar包位于：E:\demo\first-app-by-gui\target\first-app-by-gui-0.0.1-SNAPSHOT.jar目录中。


## 2.2 运行 Spring Boot 应用

### 2.2.1 spring-boot-maven-plugin打好的jar包的内部结构

打包后的jar包解压后的结构如下：
```
├─BOOT-INF
│  ├─classes
│  │  │  application.properties
│  │  │
│  │  └─thinkinginspringboot
│  │      └─firstappbygui
│  │              FirstAppByGuiApplication.class
│  │
│  └─lib
│          ....
│          spring-beans-5.2.3.RELEASE.jar
│          spring-boot-2.2.4.RELEASE.jar
│          spring-boot-autoconfigure-2.2.4.RELEASE.jar
│          ....
│
├─META-INF
│  │  MANIFEST.MF
│  │
│  └─maven
│      └─thinking-in-spring-boot
│          └─first-app-by-gui
│                  pom.properties
│                  pom.xml
│
└─org
    └─springframework
        └─boot
            └─loader
                │  ExecutableArchiveLauncher.class
                │  JarLauncher.class
                │  LaunchedURLClassLoader$UseFastConnectionExceptionsEnumeration.class
                │  ...
```
其中：
- BOOT-INF/classes目录存放应用编译后的class文件；
- BOOT-INF/lib目录存放应用依赖的JAR包；
- org/目录存放Spring Boot相关的class文件


### 2.2.2 Spring Boot 项目打成jar包后的MANIFEST.MF文件

cat META-INF/MANIFEST.MF
```
Manifest-Version: 1.0
Implementation-Title: first-app-by-gui
Implementation-Version: 0.0.1-SNAPSHOT
Start-Class: thinkinginspringboot.firstappbygui.FirstAppByGuiApplication
Spring-Boot-Classes: BOOT-INF/classes/
Spring-Boot-Lib: BOOT-INF/lib/
Build-Jdk-Spec: 1.8
Spring-Boot-Version: 2.2.4.RELEASE
Created-By: Maven Archiver 3.4.0
Main-Class: org.springframework.boot.loader.JarLauncher
```
其中的 Main-Class是JAR文件规范的标准属性，而 Start-Class属性则是Spring Boot 特有的属性

- 若打包之后为jar文件，则Main-Class的值为：org.springframework.boot.loader.JarLauncher（Jar启动器）
- 若打包之后为war文件，则Main-Class的值为：org.springframework.boot.loader.WarLauncher（War启动器）

其中的Start-Class的值是真正的引导类，META-INF/MANIFEST.MF资源中的Start-Class属性被JarLauncher（或WarLauncher）关联项目引导类。JarLauncher将BOOT-INF/lib目录下JAR文件作为引导类FirstAppByGuiApplication的类库依赖，故JarLauncher能够引导。


### 2.2.3 JarLauncher的实现原理

**通过java -jar命令引导JAR文件属于标准的可执行JAR文件，对于标准的可执行JAR文件其引导类必须位于文件MANIFEST.MF中的Main-Class属性中，而且MANIFEST.MF文件必须位于META-INF目录下；如果查看spring-boot-maven-plugin插件打包好的jar文件时，会发现在META-INF/MANIFEST.MF文件中的Main-Class属性的值是名为JarLauncher或WarLauncher，而真正的启动类位置属性Start-Class中；当对spring boot打成的包执行java -jar命令时，会执行JarLauncher类的main()方法，此方法主要做三件事，1.注册URL协议并清除应用缓存；2.设置类加载路径；3.执行Start-Class属性对应类的main方法，即真正要执行的main方法。经过这三步，spring boot会携带所需的类库依赖，引导Start-Class属性中的真正的引导类。，**

org.springframework.boot.loader.JarLauncher类所在pom文件坐标如下：
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-loader</artifactId>
	<scope>provided</scope>
</dependency>
```
Launcher的类图：

![Launcher.png](https://tlwok-online.s3.cn-north-1.jdcloud-oss.com/ihmhny/Launcher.png)

 Launcher 有一个抽象类 ExecutableArchiveLauncher ，JarLauncher 和 WarLauncher 都继承了 ExecutableArchiveLauncher

进入JarLauncher类中，执行main方法
```java
package org.springframework.boot.loader;
import org.springframework.boot.loader.archive.Archive;

public class JarLauncher extends ExecutableArchiveLauncher {

    //....

	public static void main(String[] args) throws Exception {
		new JarLauncher().launch(args);
	}

}
```
**launch()** 方法是 抽象类 **Launcher**中 实现的方法
```java
public abstract class Launcher {
    
    //...
	protected void launch(String[] args) throws Exception {
		JarFile.registerUrlProtocolHandler();
		ClassLoader classLoader = createClassLoader(getClassPathArchives());
		launch(args, getMainClass(), classLoader);
	}
```
launch方法分为三步骤:
1. 注册URL协议并清除应用缓存

2. 设置类加载路径

3. 执行main方法


#### 2.2.3.1 JarFile.registerUrlProtocolHandler()

该方法利用了 java.net.URLStreamHandler 扩展机制，其实现由 URL#getURLStreamHandler(String) 提供
```java
public class JarFile extends java.util.jar.JarFile {

    //....
	/**
	 * Register a {@literal 'java.protocol.handler.pkgs'} property so that a
	 * {@link URLStreamHandler} will be located to deal with jar URLs.
	 * 注册URL协议
	 */
	public static void registerUrlProtocolHandler() {
		String handlers = System.getProperty(PROTOCOL_HANDLER, "");
		System.setProperty(PROTOCOL_HANDLER,
				("".equals(handlers) ? HANDLERS_PACKAGE : handlers + "|" + HANDLERS_PACKAGE));
		resetCachedUrlHandlers();
	}

	/**
	 * Reset any cached handlers just in case a jar protocol has already been used. We
	 * reset the handler by trying to set a null {@link URLStreamHandlerFactory} which
	 * should have no effect other than clearing the handlers cache.
	 * 重置并清除应用缓存
	 */
	private static void resetCachedUrlHandlers() {
		try {
			URL.setURLStreamHandlerFactory(null);
		}
		catch (Error ex) {
			// Ignore
		}
	}

}
```

#### 2.2.3.2 createClassLoader(getClassPathArchives())
创建 **ClassLoader** , **getClassPathArchives()** 由子类 **ExecutableArchiveLauncher** 实现
```java
public abstract class ExecutableArchiveLauncher extends Launcher {
  //...
  protected List<Archive> getClassPathArchives() throws Exception {
   List<Archive> archives = new ArrayList<>(
     this.archive.getNestedArchives(this::isNestedArchive));
   postProcessClassPathArchives(archives);
   return archives;
  }
}
```
**isNestedArchive(Archive.Entry entry)** 需要子类 **JarLauncher** 或 **WarLauncher** 实现，以 **JarLauncher** 为例
```java
public class JarLauncher extends ExecutableArchiveLauncher {
	//...
	@Override
	protected boolean isNestedArchive(Archive.Entry entry) {
		if (entry.isDirectory()) {
			return entry.getName().equals(BOOT_INF_CLASSES);
		}
		return entry.getName().startsWith(BOOT_INF_LIB);
	}
}
```
该方法主要是为了过滤掉 **Archive.Entry** 实例是否匹配 **BOOT-INF/lib** 或 **BOOT-INF/classes** ,只要符合以上路径即可，故 **getClassPathArchives()** 的返回值还是取决于**archives** 属性对象的内容。
```java
public abstract class ExecutableArchiveLauncher extends Launcher {
  private final Archive archive;
  public ExecutableArchiveLauncher() {
    try {
      this.archive = createArchive();
    }
    catch (Exception ex) {
     throw new IllegalStateException(ex);
    }
  }
  ...
}
```
**createArchive()** 该方法来自于父类 **Launcher** ,该方法主要判断文件路径和归档文件是否正确
```java
public abstract class Launcher {
    //...
	protected final Archive createArchive() throws Exception {
		ProtectionDomain protectionDomain = getClass().getProtectionDomain();
		CodeSource codeSource = protectionDomain.getCodeSource();
		URI location = (codeSource != null ? codeSource.getLocation().toURI() : null);
		String path = (location != null ? location.getSchemeSpecificPart() : null);
		if (path == null) {
			throw new IllegalStateException("Unable to determine code source archive");
		}
		File root = new File(path);
		if (!root.exists()) {
			throw new IllegalStateException(
					"Unable to determine code source archive from " + root);
		}
		return (root.isDirectory() ? new ExplodedArchive(root)
				: new JarFileArchive(root));
	}
}
```

#### 2.2.3.3 **launch(args, getMainClass(), classLoader)**
该方法的实际执行者是 **createMainMethodRunner()**
```java
public abstract class Launcher {
    //...
	protected void launch(String[] args, String mainClass, ClassLoader classLoader)
	throws Exception {
		Thread.currentThread().setContextClassLoader(classLoader);
		createMainMethodRunner(mainClass, args, classLoader).run();
	}
	//...
	protected MainMethodRunner createMainMethodRunner(String mainClass, String[] args,
			ClassLoader classLoader) {
		return new MainMethodRunner(mainClass, args);
	}
}
```
**MainMethodRunner** 对象关联 **mainClass** 及 **main** 方法参数 **args**
```java
public class MainMethodRunner {
	//...
	public MainMethodRunner(String mainClass, String[] args) {
		this.mainClassName = mainClass;
		this.args = (args != null ? args.clone() : null);
	}
	
  	public void run() throws Exception {
		Class<?> mainClass = Thread.currentThread().getContextClassLoader()
				.loadClass(this.mainClassName);
		Method mainMethod = mainClass.getDeclaredMethod("main", String[].class);
		mainMethod.invoke(null, new Object[] { this.args });
	}
}
```
而 **mainClass** 来自 **getMainClass()**
```java
public abstract class ExecutableArchiveLauncher extends Launcher {
	...
	@Override
	protected String getMainClass() throws Exception {
		Manifest manifest = this.archive.getManifest();
		String mainClass = null;
		if (manifest != null) {
			mainClass = manifest.getMainAttributes().getValue("Start-Class");
		}
		if (mainClass == null) {
			throw new IllegalStateException(
					"No 'Start-Class' manifest entry specified in " + this);
		}
		return mainClass;
	}
}
```
类名称来自于 /META-INF/MANIFEST.MF 资源中的 Start-Class 属性，其子类没有覆盖此方法实现，故无论是JAR还是WAR，读取 Spring Boot 启动类均来自于此属性。获取**mainClass** 之后会执行 **MainMethodRunner#run()** 方法去读取 **mainClass** 类中的main(String[] args)方法
```java
// 方法一开始就展示了，为了更加清楚哪里调用，再写一遍
public abstract class Launcher {
  protected void launch(String[] args, String mainClass, ClassLoader classLoader)
    throws Exception {
   Thread.currentThread().setContextClassLoader(classLoader);
   createMainMethodRunner(mainClass, args, classLoader).run();
  }
}
```
因此 **JarLuncher** 实际上是同进程内调用 **Start-Class** 类的 **main(String[] args)** 方法，并在启动前准备好了 **Class Path**. WarLuncher 就不展开了,大部分实现逻辑如上

# 三、理解固化的 Maven 依赖

## 3.1 使用spring-boot-starter-parent作为项目的parent
这种方式是https://start.spring.io脚手架工程默认使用的方式，其缺点是当应用拥有自己的pom.xml时，就会与spring-boot-starter-parent发生冲突，为此Spring Boot提供了另一种方式：spring-boot-dependencies

## 3.2 使用spring-boot-dependencies替换单继承的限制

通过**dependencyManagement**的方式引入**spring-boot-dependencies**只解决了依赖包版本的问题，但其并不包含**spring-boot-starter-parent**中的**pluginManagement**的配置，故需要添加 **maven-war-plugin** 的配置并指定其版本号，而且在没有servlet容器的前提下，要么添加属性**failOnMissingWebXml**为**false**（表明忽略web.xml文件）、要么添加servlet3.0以上版本（可以直接添加servlet，也可以通过添加tomcat等servlet容器间接添加）；并且**spring-boot-maven-plugin**同样需要添加版本号信息，以及额外的**goal**配置为**repackage**才可以使**spring-boot-maven-plugin**插件生效！

==其实，最靠谱的方式是直接把spring-boot-starter-parent和spring-boot-dependencies中有关pluginManagement的配置添加到自己的parent工程的pom.xml文件中，这样就可以将spring-boot-starter-parent替换为自己的parent坐标而不需要进行上面的“骚操作”了。==

### 3.2.1 直接配置failOnMissingWebXml为flase的xml详情

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<!--<parent>-->
		<!--<groupId>org.springframework.boot</groupId>-->
		<!--<artifactId>spring-boot-starter-parent</artifactId>-->
		<!--<version>2.2.4.RELEASE</version>-->
		<!--<relativePath/> &lt;!&ndash; lookup parent from repository &ndash;&gt;-->
	<!--</parent>-->
	<groupId>thinking-in-spring-boot</groupId>
	<artifactId>first-app-by-gui</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>first-app-by-gui</name>
	<packaging>war</packaging>
	<description>Demo project for Spring Boot</description>

	<properties>
		<java.version>1.8</java.version>
		<junit.version>4.12</junit.version>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<maven.compiler.source>${java.version}</maven.compiler.source>
		<maven.compiler.target>${java.version}</maven.compiler.target>
		<maven-war-plugin.version>3.2.3</maven-war-plugin.version>
		<maven-compiler-plugin.version>3.8.1</maven-compiler-plugin.version>
		<spring-boot-dependencies.version>2.2.4.RELEASE</spring-boot-dependencies.version>
		<spring-boot-maven-plugin.version>${spring-boot-dependencies.version}</spring-boot-maven-plugin.version>
	</properties>

	<dependencyManagement>
		<dependencies>
			<!--
			此方式仅关注 dependencyManagement不关注plugin，
			故其使用的maven-war-plugin的版本为2.2
			故需要手动添加maven-war-plugin并重新指定版本号
			-->
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-dependencies</artifactId>
				<version>${spring-boot-dependencies.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-webflux</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-loader</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>

		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<!-- 保持与 spring-boot-dependencies 版本一致 -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>${maven-compiler-plugin.version}</version>
				<configuration>
					<source>${java.version}</source>
					<target>${java.version}</target>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-war-plugin</artifactId>
				<version>${maven-war-plugin.version}</version>
				<!-- TODO 书中的说法不需要添加这个configuration的，原因有待验证！！ -->
				<configuration>
					<failOnMissingWebXml>false</failOnMissingWebXml>
				</configuration>
			</plugin>
			<plugin>
				<!--
					该插件在使用spring-boot-dependencies时，需要：
					1. 指定其版本号（与spring-boot-dependencies一致）
					2. 需要添加goal标签且其值为“repackage”
				 -->
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<version>${spring-boot-maven-plugin.version}</version>
				<executions>
					<execution>
						<goals>
							<goal>repackage</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>

</project>

```

### 3.2.2 直接添加servlet的xml详情

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<!--<parent>-->
		<!--<groupId>org.springframework.boot</groupId>-->
		<!--<artifactId>spring-boot-starter-parent</artifactId>-->
		<!--<version>2.2.4.RELEASE</version>-->
		<!--<relativePath/> &lt;!&ndash; lookup parent from repository &ndash;&gt;-->
	<!--</parent>-->
	<groupId>thinking-in-spring-boot</groupId>
	<artifactId>first-app-by-gui</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>first-app-by-gui</name>
	<packaging>war</packaging>
	<description>Demo project for Spring Boot</description>

	<properties>
		<java.version>1.8</java.version>
		<javax.servlet-api.version>4.0.1</javax.servlet-api.version>
		<junit.version>4.12</junit.version>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<maven.compiler.source>${java.version}</maven.compiler.source>
		<maven.compiler.target>${java.version}</maven.compiler.target>
		<maven-war-plugin.version>3.2.3</maven-war-plugin.version>
		<maven-compiler-plugin.version>3.8.1</maven-compiler-plugin.version>
		<spring-boot-dependencies.version>2.2.4.RELEASE</spring-boot-dependencies.version>
		<spring-boot-maven-plugin.version>${spring-boot-dependencies.version}</spring-boot-maven-plugin.version>
	</properties>

	<dependencyManagement>
		<dependencies>
			<!--
			此方式仅关注 dependencyManagement不关注plugin，
			故其使用的maven-war-plugin的版本为2.2
			故需要手动添加maven-war-plugin并重新指定版本号
			-->
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-dependencies</artifactId>
				<version>${spring-boot-dependencies.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

	<dependencies>

		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>${javax.servlet-api.version}</version>
			<scope>provided</scope>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-webflux</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-loader</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>

		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<!-- 保持与 spring-boot-dependencies 版本一致 -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>${maven-compiler-plugin.version}</version>
				<configuration>
					<source>${java.version}</source>
					<target>${java.version}</target>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-war-plugin</artifactId>
				<version>${maven-war-plugin.version}</version>
			</plugin>
			<plugin>
				<!--
					该插件在使用spring-boot-dependencies时，需要：
					1. 指定其版本号（与spring-boot-dependencies一致）
					2. 需要添加goal标签且其值为“repackage”
				 -->
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<version>${spring-boot-maven-plugin.version}</version>
				<executions>
					<execution>
						<goals>
							<goal>repackage</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>

</project>

```
### 3.2.3 通过添加servlet容器间接添加servlet的xml详情

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<!--<parent>-->
		<!--<groupId>org.springframework.boot</groupId>-->
		<!--<artifactId>spring-boot-starter-parent</artifactId>-->
		<!--<version>2.2.4.RELEASE</version>-->
		<!--<relativePath/> &lt;!&ndash; lookup parent from repository &ndash;&gt;-->
	<!--</parent>-->
	<groupId>thinking-in-spring-boot</groupId>
	<artifactId>first-app-by-gui</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>first-app-by-gui</name>
	<packaging>war</packaging>
	<description>Demo project for Spring Boot</description>

	<properties>
		<java.version>1.8</java.version>
		<javax.servlet-api.version>4.0.1</javax.servlet-api.version>
		<junit.version>4.12</junit.version>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<maven.compiler.source>${java.version}</maven.compiler.source>
		<maven.compiler.target>${java.version}</maven.compiler.target>
		<maven-war-plugin.version>3.2.3</maven-war-plugin.version>
		<maven-compiler-plugin.version>3.8.1</maven-compiler-plugin.version>
		<spring-boot-dependencies.version>2.2.4.RELEASE</spring-boot-dependencies.version>
		<spring-boot-maven-plugin.version>${spring-boot-dependencies.version}</spring-boot-maven-plugin.version>
	</properties>

	<dependencyManagement>
		<dependencies>
			<!--
			此方式仅关注 dependencyManagement不关注plugin，
			故其使用的maven-war-plugin的版本为2.2
			故需要手动添加maven-war-plugin并重新指定版本号
			-->
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-dependencies</artifactId>
				<version>${spring-boot-dependencies.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

	<dependencies>

		<!-- Tomcat -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-webflux</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-loader</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>

		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<!-- 保持与 spring-boot-dependencies 版本一致 -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>${maven-compiler-plugin.version}</version>
				<configuration>
					<source>${java.version}</source>
					<target>${java.version}</target>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-war-plugin</artifactId>
				<version>${maven-war-plugin.version}</version>
			</plugin>
			<plugin>
				<!--
					该插件在使用spring-boot-dependencies时，需要：
					1. 指定其版本号（与spring-boot-dependencies一致）
					2. 需要添加goal标签且其值为“repackage”
				 -->
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<version>${spring-boot-maven-plugin.version}</version>
				<executions>
					<execution>
						<goals>
							<goal>repackage</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>

</project>

```



# 四、理解嵌入式Web容器

四种嵌入式web容器，Tomcat、Jetty、Undertow以及Netty Web Server(2.0+才有)

## 4.1 嵌入式 Servlet Web容器

Spring Boot版本 | Servlet Name | Servlet Version | Java Version
---|---|---|---
Spring Boot 2.0 | Tomcat 8.5 | 3.1 | Java 8+
Spring Boot 2.0 | Jetty 9.4 | 3.1 | Java 8+
Spring Boot 2.0 | Undertow 1.4 | 3.1 | Java 8+
Spring Boot 1.5 | Tomcat 8 | 3.1 | Java 7+
Spring Boot 1.5 | Tomcat 7 | 3.0 | Java 6+
Spring Boot 1.5 | Jetty 9.3 | 3.1 | Java 8+
Spring Boot 1.5 | Jetty 9.2 | 3.1 | Java 7+
Spring Boot 1.5 | Jetty 8 | 3.0 | Java 6+
Spring Boot 1.5 | Undertow 1.3 | 3.1 | Java 7+

### 4.1.1 Tomcat 作为嵌入式Servlet Web容器

**Spring Boot FAT JAR 或 Spring Boot FAT WAR 与 Tomcat Maven插件的对比。**

Spring Boot 默认情况下使用就是tomcat嵌入式容器，只需要添加 spring-boot-starter-web插件即可实现 tomcat嵌入式容器的加载
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
其org.springframework.boot.web.server.WebServer实现为：**org.springframework.boot.web.embedded.tomcat.TomcatWebServer**


The Apache Tomcat Maven Plugin

https://tomcat.apache.org/maven-plugin.html

目前最新版本为

```xml
<!-- https://mvnrepository.com/artifact/org.apache.tomcat.maven/tomcat7-maven-plugin -->
<!-- tomcat7 官方插件 -->
<dependency>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
</dependency>


<!-- https://mvnrepository.com/artifact/org.apache.tomcat.maven/tomcat8-maven-plugin -->
<!-- tomcat8 官方插件 -->
<dependency>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat8-maven-plugin</artifactId>
    <version>2.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.apache.tomcat.maven/tomcat8-maven-plugin -->
<dependency>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat8-maven-plugin</artifactId>
    <version>3.0-r1756463</version>
</dependency>
```

### 4.1.2 Jetty 作为嵌入式Servlet Web容器
- 使用maven

```xml
<properties>
    <servlet-api.version>3.1.0</servlet-api.version>
</properties>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <!-- Exclude the Tomcat dependency -->
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<!-- Use Jetty instead -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```
- 使用Gradle

```properties
configurations {
// exclude Tomcat Web Server
compile.exclude module: 'spring-boot-starter-tomcat'
}
dependencies {
compile 'org.springframework.boot:spring-boot-starter-web'
// Use Jetty instead
compile 'org.springframework.boot:spring-boot-starter-jetty'
```

其org.springframework.boot.web.server.WebServer实现为：**org.springframework.boot.web.embedded.jetty.JettyWebServer**

### 4.1.3 Undertow 作为嵌入式Servlet Web容器
```xml
<properties>
    <servlet-api.version>3.1.0</servlet-api.version>
</properties>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <!-- Exclude the Tomcat dependency -->
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<!-- Use Jetty instead -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-undertow</artifactId>
</dependency>
```

其org.springframework.boot.web.server.WebServer实现为：**org.springframework.boot.web.embedded.undertow.UndertowServletWebServer**

## 4.2 嵌入式Reactive Web容器

==当spring-boot-starter-webflux和spring-boot-starter-web同时存在时，spring boot 会忽略webflux，直接使用spring-boot-starter-web==

启动一个reactive application，需要去掉spring-boot-starter-web依赖并添加spring-boot-starter-webflux依赖。默认情况下，使用Netty Web Server作为其web容器，其pom配置为：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```
其org.springframework.boot.web.server.WebServer实现为：：**org.springframework.boot.web.embedded.netty.NettyWebServer**


### 4.2.1 undertow作为嵌入式ReactiveWeb容器

- pom配置为

```xml
<!-- WebFlux依赖 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>

<!-- Use Undertow instead -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-undertow</artifactId>
</dependency>
```

- 通过代码验证webflux是否启动成功以及当前的WebServer是否为期望的undertow

通过 WebServerInitializedEvent 可以获取运行的 webserver相关的信息，比如WebServer的实现类，http端口号等信息。

```java

import org.springframework.boot.ApplicationArguments;
import org.springframework.boot.ApplicationRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.web.context.WebServerApplicationContext;
import org.springframework.boot.web.context.WebServerInitializedEvent;
import org.springframework.context.annotation.Bean;
import org.springframework.context.event.EventListener;
import org.springframework.web.reactive.function.server.RequestPredicates;
import org.springframework.web.reactive.function.server.RouterFunction;
import org.springframework.web.reactive.function.server.RouterFunctions;
import org.springframework.web.reactive.function.server.ServerResponse;
import reactor.core.publisher.Mono;


@SpringBootApplication
public class SpringBootDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBootDemoApplication.class, args);
    }

    @Bean
    public RouterFunction<ServerResponse> helloWorld() {
        return RouterFunctions.route(
                RequestPredicates.GET("/hello-world"),
                request -> ServerResponse.ok().body(Mono.just("Hello, World"), String.class));
    }

    /**
     * 该方法只考虑了Servlet和Reactive两种Web场景，并没有考虑非Web应用类型
     * {@link ApplicationRunner#run(ApplicationArguments)} 方法在Spring Boot应用启动后回调
     * @param context
     * @return
     */
    @Bean
    public ApplicationRunner runner(WebServerApplicationContext context) {
        return args -> {
            System.out.println("1当前 WebServer 实现类为：" + context.getWebServer().getClass().getName());
            System.out.println("1当前 WebServer 端口号为：" + context.getWebServer().getPort());
        };
    }

    /**
     * 该方法适用于 Web及非Web应用，相比 注入 {@link WebServerApplicationContext} 更加健壮
     * 参见 spring boot 官方文档：78.5 Discover the HTTP Port at Runtime
     * @param event
     */
    @EventListener(WebServerInitializedEvent.class)
    public void onWebServerReady(WebServerInitializedEvent event) {
        System.out.println("2当前 WebServer 实现类为：" + event.getWebServer().getClass().getName());
        System.out.println("2当前 WebServer 端口号为：" + event.getWebServer().getPort());
    }

}

```
其org.springframework.boot.web.server.WebServer实现为：：**org.springframework.boot.web.embedded.undertow.UndertowWebServer**

### 4.2.2 Jetty 作为嵌入式Reactive Web容器

添加jetty相关的starter，其pom文件如下所示：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```

其org.springframework.boot.web.server.WebServer实现为：：**org.springframework.boot.web.embedded.jetty.JettyWebServer**

### 4.2.3 Tomcat 作为嵌入式Reactive Web容器

添加tomcat相关的starter，其pom文件如下所示：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```

其org.springframework.boot.web.server.WebServer实现为：：**org.springframework.boot.web.embedded.jetty.TomcatWebServer**


# 第五章 理解自动装配

参见 ++《Spring Boot Reference Guide》16. Auto-configuration++

装配@Configuration的方法：
- xml元素<context:component-scan>
- 注解@Import
- 注解@ComponentScan

在 **@Configuration** 注解的类上添加 **@EnableAutoConfiguration** 或者 **@SpringBootApplication** 注解即可激活自动装配。

通过在配置文件中配置```logging.level.root=debug```可以查看当前应用自动装配的加载情况及原因

- 如何禁止特定的一些类的自动装配

两种方法：
1. 使用 @EnableAutoConfiguration注解，其有两个属性，exclude 和 excludeName，前者指定一个Class，后者需要一个Class的全路径名。
2. 在配置文件中配置```sping.autoconfigure.exclude=...```。

**可以两种方法同时使用**

## 5.1 理解@SpringBootApplication注解语义

在 1.3.8版本中

```java
package org.springframework.boot.autoconfigure;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Inherited;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.annotation.AliasFor;

/**
 * Indicates a {@link Configuration configuration} class that declares one or more
 * {@link Bean @Bean} methods and also triggers {@link EnableAutoConfiguration
 * auto-configuration} and {@link ComponentScan component scanning}. This is a convenience
 * annotation that is equivalent to declaring {@code @Configuration},
 * {@code @EnableAutoConfiguration} and {@code @ComponentScan}.
 *
 * @author Phillip Webb
 * @author Stephane Nicoll
 * @since 1.2.0
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@Configuration
@EnableAutoConfiguration
@ComponentScan
public @interface SpringBootApplication {

	/**
	 * Exclude specific auto-configuration classes such that they will never be applied.
	 * @return the classes to exclude
	 */
	Class<?>[] exclude() default {};

	/**
	 * Exclude specific auto-configuration class names such that they will never be
	 * applied.
	 * @return the class names to exclude
	 * @since 1.3.0
	 */
	String[] excludeName() default {};

	/**
	 * Base packages to scan for annotated components. Use {@link #scanBasePackageClasses}
	 * for a type-safe alternative to String-based package names.
	 * @return base packages to scan
	 * @since 1.3.0
	 */
	@AliasFor(annotation = ComponentScan.class, attribute = "basePackages")
	String[] scanBasePackages() default {};

	/**
	 * Type-safe alternative to {@link #scanBasePackages} for specifying the packages to
	 * scan for annotated components. The package of each class specified will be scanned.
	 * <p>
	 * Consider creating a special no-op marker class or interface in each package that
	 * serves no purpose other than being referenced by this attribute.
	 * @return base packages to scan
	 * @since 1.3.0
	 */
	@AliasFor(annotation = ComponentScan.class, attribute = "basePackageClasses")
	Class<?>[] scanBasePackageClasses() default {};

}
```

在 1.4.0.RELEASE版本中变成了(其中TypeExcludeFilter是1.4.0引入springboot的，用于查找BeanFactory中已注册的TypeExcludeFilter Bean，作为代理执行对象)
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class))
public @interface SpringBootApplication {
    //...
}
```
在 1.5.0.RELEASE版本中变成了(其中AutoConfigurationExcludeFilter是1.5.0引入springboot的，用于排除其他同时标注@Configuration和@EnableAutoConfiguration的类)
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
    //...
}
```
从 2.2.X版本开始在类中添加了 proxyBeanMethods 方法
```java
	/**
	 * Specify whether {@link Bean @Bean} methods should get proxied in order to enforce
	 * bean lifecycle behavior, e.g. to return shared singleton bean instances even in
	 * case of direct {@code @Bean} method calls in user code. This feature requires
	 * method interception, implemented through a runtime-generated CGLIB subclass which
	 * comes with limitations such as the configuration class and its methods not being
	 * allowed to declare {@code final}.
	 * <p>
	 * The default is {@code true}, allowing for 'inter-bean references' within the
	 * configuration class as well as for external calls to this configuration's
	 * {@code @Bean} methods, e.g. from another configuration class. If this is not needed
	 * since each of this particular configuration's {@code @Bean} methods is
	 * self-contained and designed as a plain factory method for container use, switch
	 * this flag to {@code false} in order to avoid CGLIB subclass processing.
	 * <p>
	 * Turning off bean method interception effectively processes {@code @Bean} methods
	 * individually like when declared on non-{@code @Configuration} classes, a.k.a.
	 * "@Bean Lite Mode" (see {@link Bean @Bean's javadoc}). It is therefore behaviorally
	 * equivalent to removing the {@code @Configuration} stereotype.
	 * @since 2.2
	 * @return whether to proxy {@code @Bean} methods
	 */
	@AliasFor(annotation = Configuration.class)
	boolean proxyBeanMethods() default true;
```

**@SpringBootApplication** 被用于激活 **@EnableAutoConfiguration** 、 **@ComponentScan** 和 **@Configuration** 三个注解语义。

- @EnableAutoConfiguration：负责激活Spring Boot自动装配机制
- @ComponentScan：负责激活@Component扫描
- @Configuration：负责标注该类为配置类以允许在上下文中注入其他的Bean或导入其他配置

@SpringBootConfiguration属于多层次的@Component“派生”注解，叫做“Spring模式注解（Stereotype Annotations）”

## 5.2 @SpringBootApplication 属性别名

@AliasFor的注解编程模型在文章[Spring Annotation Programming Model](https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model)中的[Attribute Aliases and Overrides](https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model#attribute-aliases-and-overrides)中有详情说明

- Implicit Aliases 隐式覆盖
如果注解@One中有一个属性A，注解@Two中也有一个属性A，而@Two是@One的元注解，则@One中的A就会覆盖@Two中的A，此为隐式覆盖
- Explicit Aliases 显式覆盖
如果通过@AliasFor在元注释中将属性A声明为属性B的别名，则A是B的显式替代。
- Transitive Explicit Aliases 传递性显式覆盖
如果注解@One中的属性A是对注解@Two中属性B的显式覆盖，而B是注解@Three中的属性C的显式覆盖，则A是遵循传递性定律的C的传递性显式覆盖。

```java
import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Inherited;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import org.springframework.boot.SpringBootConfiguration;
import org.springframework.boot.context.TypeExcludeFilter;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.ComponentScan.Filter;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.FilterType;
import org.springframework.core.annotation.AliasFor;
import org.springframework.data.repository.Repository;

/**
 * Indicates a {@link Configuration configuration} class that declares one or more
 * {@link Bean @Bean} methods and also triggers {@link EnableAutoConfiguration
 * auto-configuration} and {@link ComponentScan component scanning}. This is a convenience
 * annotation that is equivalent to declaring {@code @Configuration},
 * {@code @EnableAutoConfiguration} and {@code @ComponentScan}.
 *
 * @author Phillip Webb
 * @author Stephane Nicoll
 * @author Andy Wilkinson
 * @since 1.2.0
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
    
    /**
     * Implicit Aliases 隐式覆盖
     */
	@AliasFor(annotation = EnableAutoConfiguration.class)
	Class<?>[] exclude() default {};

    /**
     * Implicit Aliases 隐式覆盖
     */
	@AliasFor(annotation = EnableAutoConfiguration.class)
	String[] excludeName() default {};

    /**
     * Explicit Aliases 显式覆盖
     */
	@AliasFor(annotation = ComponentScan.class, attribute = "basePackages")
	String[] scanBasePackages() default {};
	
    /**
     * Explicit Aliases 显式覆盖
     */
	@AliasFor(annotation = ComponentScan.class, attribute = "basePackageClasses")
	Class<?>[] scanBasePackageClasses() default {};

    /**
     * Implicit Aliases 隐式覆盖
     */
	@AliasFor(annotation = Configuration.class)
	boolean proxyBeanMethods() default true;

}

```

## 5.3 @SpringBootApplication标注非引导类

@SpringBootApplication并非只能标注在引导类上，同样标注在非引导类上同样可以正常使用spring boot

- 项目结构如下：tree /F
```
E:.
├─java
│  └─com
│      └─xiaobei
│          └─java
│              └─demo
│                  ├─config
│                  │      WebConfig.java
│                  │
│                  └─springbootdemo
│                          SpringBootDemoApplication.java
│
└─resources
    │  application.properties
    │
    ├─static
    └─templates
```

- WebConfig.java
```
package com.xiaobei.java.demo.config;

import org.springframework.boot.ApplicationArguments;
import org.springframework.boot.ApplicationRunner;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.web.context.WebServerApplicationContext;
import org.springframework.boot.web.context.WebServerInitializedEvent;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.event.EventListener;
import org.springframework.web.reactive.function.server.RequestPredicates;
import org.springframework.web.reactive.function.server.RouterFunction;
import org.springframework.web.reactive.function.server.RouterFunctions;
import org.springframework.web.reactive.function.server.ServerResponse;
import reactor.core.publisher.Mono;

/**
 * @author <a href="https://github.com/xiaobei-ihmhny">xiaobei-ihmhny</a>
 * @date 2020-02-18 09:06:06
 */
//@Configuration
@SpringBootApplication
public class WebConfig {

    @Bean
    public RouterFunction<ServerResponse> helloWorld() {
        return RouterFunctions.route(
                RequestPredicates.GET("/hello-world"),
                request -> ServerResponse.ok().body(Mono.just("Hello, World"), String.class));
    }

    /**
     * 该方法只考虑了Servlet和Reactive两种Web场景，并没有考虑非Web应用类型
     * {@link ApplicationRunner#run(ApplicationArguments)} 方法在Spring Boot应用启动后回调
     * @param context
     * @return
     */
    @Bean
    public ApplicationRunner runner(WebServerApplicationContext context) {
        return args -> {
            System.out.println("1当前 WebServer 实现类为：" + context.getWebServer().getClass().getName());
            System.out.println("1当前 WebServer 端口号为：" + context.getWebServer().getPort());
        };
    }

    /**
     * 该方法适用于 Web及非Web应用，相比 注入 {@link WebServerApplicationContext} 更加健壮
     * @param event
     */
    @EventListener(WebServerInitializedEvent.class)
    public void onWebServerReady(WebServerInitializedEvent event) {
        System.out.println("2当前 WebServer 实现类为：" + event.getWebServer().getClass().getName());
        System.out.println("2当前 WebServer 端口号为：" + event.getWebServer().getPort());
    }
}

```

- SpringBootDemoApplication.java

```java
package com.xiaobei.java.demo.springbootdemo;

import com.xiaobei.java.demo.config.WebConfig;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;


//@SpringBootApplication(scanBasePackages = "com.xiaobei.java.demo.config")
public class SpringBootDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(WebConfig.class, args);
    }


}
```
## 5.4 @EnableAutoConfiguration激活自动配置

将 5.3节中的@SpringBootApplication注解改为@EnableAutoConfiguration同样可以激活自动配置，这两个注解在激动自动装配上没有差别，但对于被标注类的Bean类型则存在差异。


## 5.5 @SpringBootApplication 继承 @Configuration CGLIB提升特性
给WebConfig类添加Bean类型输出，代码如下
```java
package com.xiaobei.java.demo.config;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.boot.ApplicationRunner;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.reactive.function.server.RequestPredicates;
import org.springframework.web.reactive.function.server.RouterFunction;
import org.springframework.web.reactive.function.server.RouterFunctions;
import org.springframework.web.reactive.function.server.ServerResponse;
import reactor.core.publisher.Mono;

/**
 * @author <a href="https://github.com/xiaobei-ihmhny">xiaobei-ihmhny</a>
 * @date 2020-02-18 09:06:06
 */
//@EnableAutoConfiguration
//@Configuration
//@SpringBootApplication
public class WebConfig {

    @Bean
    public RouterFunction<ServerResponse> helloWorld() {
        return RouterFunctions.route(
                RequestPredicates.GET("/hello-world"),
                request -> ServerResponse.ok().body(Mono.just("Hello, World"), String.class));
    }
    
    @Bean
    public ApplicationRunner runner(BeanFactory beanFactory) {
        return args -> {
            System.out.println("当前 helloWorld Bean 实现类为：" + beanFactory.getBean("helloWorld").getClass().getName());
            System.out.println("当前 WebConfig Bean 实现类为：" + beanFactory.getBean(WebConfig.class).getClass().getName());
        };
    }


}

```

1. 当使用@EnableAutoConfiguration时运行结果如下：

```text
当前 helloWorld Bean 实现类为：org.springframework.web.reactive.function.server.RouterFunctions$DefaultRouterFunction
当前 WebConfig Bean 实现类为：com.xiaobei.java.demo.config.WebConfig
```

2. 当使用@SpringBootApplication时运行结果如下：

```text
当前 helloWorld Bean 实现类为：org.springframework.web.reactive.function.server.RouterFunctions$DefaultRouterFunction
当前 WebConfig Bean 实现类为：com.xiaobei.java.demo.config.WebConfig$$EnhancerBySpringCGLIB$$ba2077ad
```

1和2对比可以发现，所谓的CGLIB提升并非是为@Bean对象提供的，而是为@Configuration类准备的。


## 5.6 理解自动配置机制
**@ConditionalOnClass** 和 **@ConfitionalOnMissingBean** 是最常见的注解，当 **@ConditionalOnClass** 标注在 **@Configuraton** 类上时，当且仅当目标类存在于 **ClassPath** 下时才予以装配。

如何自定义自己的自动装配类呢？
1. 在resources目录下创建特定文件，路径固定为：**META-INF/spring.factories**，将自己的自动装配类放入该属性配置文件中，基key为固定的：**org.springframework.boot.autoconfigure.EnableAutoConfiguration**，自己类的全路径名为该key的value，多个时以","分隔，即可完成自定义自动配置类的配置，如下所示：
```properties
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.tlwok.sso.autoconfigure.SsoAutoConfiguration
```
注意：自定义类以 **AutoConfiguration** 结尾。


## 5.7 创建自动配置类
调整当前项目结构如下：
```
├─java
│  └─com
│      └─xiaobei
│          └─java
│              └─demo
│                  ├─autoconfigure
│                  │      WebAutoConfiguration.java
│                  │
│                  ├─config
│                  │      WebConfig.java
│                  │
│                  └─springbootdemo
│                          SpringBootDemoApplication.java
│
└─resources
    │  application.properties
    │
    ├─META-INF
    │      spring.factories
    │
    ├─static
    └─templates
```

其中相关类中注解及文件的配置如下：
```java
// WebAutoConfiguration.java
-----
package com.xiaobei.java.demo.autoconfigure;
import com.xiaobei.java.demo.config.WebConfig;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

/**
 * @author <a href="https://github.com/xiaobei-ihmhny">xiaobei-ihmhny</a>
 * @date 2020-02-18 22:54:54
 */
@Configuration
@Import(WebConfig.class)
public class WebAutoConfiguration {
}
-----

// WebConfig.java
-----
@Configuration
public class WebConfig {
    //....
}
-----

// SpringBootDemoApplication.java
-----
package com.xiaobei.java.demo.springbootdemo;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication
public class SpringBootDemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringBootDemoApplication.class, args);
    }
}


// spring.factories
-----
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.xiaobei.java.demo.autoconfigure.WebAutoConfiguration
```
同时为了支持以配置化的方式调整应用行为，如Web服务端口等，Spring Boot提供了Production-Ready特性

# 第六章 理解 Production-Ready 特性

官方文档首页有关 Production-Ready 的介绍：

**Provide production-ready features such as metrics, health checks and externalized configuration**

## 6.1 理解 Production-Reday 一般性定义
Production-Ready是DevOps的立足点，来自：http://12factor.net/，


## 6.2 理解Spring Boot Actuator

官方文档对Production-Ready的描述主要如下

- 使用场景：监视和管理投入生产的应用
- 监管媒介：HTTP或JMX端点（Endpoints）
- 端点类型：审计（Auditing）、健康（Health）和指标收集（metrics gathering）
- 基本特点：自动运用（automatically applied）

## 6.3 Spring Boot Actuator Endpoints

在 文档 spring-boot-reference-2.1.3.RELEASE.pdf 中列出了常见的endpoints（53. Endpoints）
- beans：显示当前Spring应用上下文的Spring Bean完整列表
- conditions：显示在配置类和自动配置类上评估的条件以及它们匹配或不匹配的原因
- env：暴露Spring ConfigurableEnvironment中的PropertySource属性
- health：显示应用的健康信息
- info：显示任意的应用信息

若想开启 Spring Boot Actuator 需要添加相关依赖
```xml
<!-- spring boot actuator 依赖 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
默认情况下只暴露了health和info的Web Endpoints，如需要暴露其他的端点，可以通过属性：management.endpoints.web.exposure.include=*来配置，多个端点之间用","号隔开。此外的配置遵循SpringBoot外部化配置的优先级（24. Externalized Configuration）。

通过类似这样的请求来访问：http://localhost:8080/actuator/conditions


## 6.4 理解“外部化配置”

在 文档 spring-boot-reference-2.1.3.RELEASE.pdf 中有专门的章节（24. Externalized Configuration）介绍外部化配置，链接：[24. Externalized Configuration](https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/reference/htmlsingle/#boot-features-external-config)
在大纲中主要说了两个问题：一个是外部化配置都有哪些及其优先级，另一个是项目中如何使用这些配置。

1. 外部化配置由高到低的优先级如下：

-  1.Devtools global setting properties on your home directory（when devtools is active）

说明：在springboot 2.1.3.RELEASE中这个home目录为：~/.spring-boot-devtools.properties，而在springboot 2.2.5.RELEASE中这个Home目录变成了：$HOME/.config/spring-boot folder

- 2 

2. 如何使用这些配置

springboot官方文档之 外部化配置学习，这段大纲主要说了两个事情，一个是springboot所支持的外部化配置都有哪些以及他们的优先级，另一个是项目中如何使用这些配置。
对于第一个事情，文档中共列举了17中外部化配置，比较常用的有 4.命令行 9.java系统变量 10. 系统变量（主要用于服务器端）还有13.通过application-{profile}.properties来区分不同环境，以及15. application.properties作为总配置。

对于第二事情，@Value应该是最常用的，但@Value并不适用于所有的情况，因为@Value是通过类org.springframework.beans.factory.config.PropertyPlaceholderConfigurer来加载的，所有@Value只适用于加载顺序在PropertyPlaceholderConfigurer之后的类，比如我们在使用mybatis时，类org.mybatis.spring.mapper.MapperScannerConfigurer的加载顺序就先于PropertyPlaceholderConfigurer加载，此时就无法使用@Value，可以使用Environment，Environment一般可以通过实现类org.springframework.context.EnvironmentAware并重写其com.tlwok.common.master.dao.MasterDataSourceConfig#setEnvironment方法来获取应用的environment，进而通过environment.getProperty('')来获取配置中的属性值。而@ConfigurationProperties一般可以用于生成IDE辅助信息，可以在使用者输入相关属性时给出智能提示。


## 6.5 理解“规约大于配置”
在springboot官网描述的最后一个特性为：
```
Absolutely no code generation and no requirement for XML configuration.
```
意思是：完全没有代码生成，也不需要xml配置
后半句也就是所谓的“规约大于配置”。其中Spring Framework是Spring Boot的“基础设施”，Spring Boot的基本特性均来自于Spring Framework。

回顾一下Spring注解的发展历程：

从Spring Framework 2.5 开始，Spring Bean注册方式由Annotation驱动逐步替代XML文件驱动。增加了@Compoent及“派生”注解（如@Service）与XML元素```<context:component-scan base-package="">```相互配合，将 @Component Bean扫描并注册至Spring Bean容器（BeanFactory），通过DI注解@Autowired获取相应的Spring组件Bean。然而此时，@Component Bean必须在```<context:component-scan>```规定的base-package集合范围中。

到了Spring Framework 3.0时代，新引入的Annotation @Configuration是xml配置文件的替代物。而Bean的定义不再需要在XML文件中声明```<bean>```元素，可使用@Bean来代替。同时，框架提供了更细粒度的Annotation @Import来导入@Configuration Class，将其注册为Spring Bean，并进一步解析其声明的Spring Bean注册相关的的注解。如@Import或@Bean。尽管在Bean的装配方面有明显提升，但此时仍是以硬编码的方式指定范围。

当Spring Framework 3.1发布后，带来了相当大的更新。此时的Spring注解可以才完全取代XML配置文件，引入了Annotation @ComponentSCan来代替XML元素```<context:component-scan>```，应用方可以实现ImportSelector接口（实现selectImports(AnnotationMetadata)方法），程序动态地决定哪些Spring Bean需要被导入。但是ImportSelector实现类必须暴露成Spring Bean，否则selectImports(AnnotaionMetadata)方法不会被Spring容器调用。为了简化配置，Spring Framework 3.1内建了不少的功能“模块”激活的注解，如@EnableCaching、@EnableAspectJAutoProxy、@EnableAsync、@EnableScheduling等。即使如此被标注的这些激活注解的类同样需要通过@ComponentScan或@Import等方式被Spring容器感知。硬编码的问题得到了缓解，但仍然与自动装配的能力相去甚远。

Spring Framework到了4.0版本增加了条件化的Spring Bean装配注解@Conditional，其value()属性可指定Condition的实现类，而Condition提供装配条件的实现逻辑，@Conditional的引入更直观表达了Spring Bean装载时所需的前置条件。正因为@Conditional的引入，使得条件性装配成为可能。Spring Boot在此基础上，实现了最显著的特性之一——条件化自动装配。


# 疑问
1. 在 2.2.3.1 JarFile.registerUrlProtocolHandler() 中的“该方法利用了 java.net.URLStreamHandler 扩展机制，其实现由 URL#getURLStreamHandler(String) 提供”如何理解？
2. **org.springframework.boot.loader.Launcher#createArchive**的实现内容不懂！！！
3. 《Spring Boot 编程思想》 p47-50页，不太懂！！！
4. tomcat maven插件如何将应用打包成JAR或WAR文件并通过java -jar 直接驱动尚未测试通过，后期需要进一步研究。
5. 在5.1中需要进一步学习 **org.springframework.boot.context.TypeExcludeFilter** 和 **org.springframework.boot.autoconfigure.AutoConfigurationExcludeFilter** 的作用，参见《Spring Boot 编程思想（核心篇）》P100-101
6. @AliasFor的注解编程模型在文章[Spring Annotation Programming Model](https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model)中的[Attribute Aliases and Overrides](https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model#attribute-aliases-and-overrides)中有详情说明
7. 12factor.net待学习
8. 


