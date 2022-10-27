# Example Maven multi-module project by parent relative path

本项目为 Java 模块测试项目

## 模块化方式：

在父模块中不配置子模块信息，在子模块中使用<parent>标签通过相对路径指定父模块

### 父模块 pom.xml

```xml
  <groupId>seal.io</groupId>
  <artifactId>example-root</artifactId>
  <version>2.0-SNAPSHOT</version>
  <name>example-root</name>
  <!-- pom 打包方式代表父工程是一个aggregator工程 -->
  <packaging>pom</packaging>
```

### 子模块 pom.xml

Module 1:

```xml
  <!-- 继承父pom文件 -->
  <parent>
    <groupId>seal.io</groupId>
    <artifactId>example-root</artifactId>
    <version>2.0-SNAPSHOT</version>
    <!-- 指明父pom的位置，<relativePath>标签，如果pom的层次关系只隔一层，则可以省略这个。maven同样可以找到子pom。-->
    <relativePath>../pom.xml</relativePath>
  </parent>

  <!-- 子模块pom，groupID和version使用父模块的 -->
  <artifactId>module1</artifactId>
  <name>module1</name>

   <!-- 子模块module1包含有漏洞的log4j -->
  <dependencies>
    <dependency>
      <groupId>org.apache.logging.log4j</groupId>
      <artifactId>log4j-core</artifactId>
      <version>2.15.0</version>
    </dependency>
  </dependencies>
```

Module 2:

```xml
   <!-- 继承父pom文件 -->
  <parent>
    <groupId>seal.io</groupId>
    <artifactId>example-root</artifactId>
    <version>2.0-SNAPSHOT</version>
    <relativePath>../pom.xml</relativePath>
  </parent>

  <!-- 子模块pom，groupID和version使用父模块的 -->
  <artifactId>module1</artifactId>
  <name>module2</name>

 <!-- 子模块module2包含有漏洞的另一版本的log4j -->
  <dependencies>
    <dependency>
      <groupId>org.apache.logging.log4j</groupId>
      <artifactId>log4j-core</artifactId>
      <version>2.12.0</version>
    </dependency>
  </dependencies>
```
