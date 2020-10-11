<link rel="stylesheet" href="https://zhmhbest.gitee.io/hellomathematics/style/index.css">
<script src="https://zhmhbest.gitee.io/hellomathematics/style/index.js"></script>

# [Maven](../index.html)

[TOC]

## 安装

### 文件目录

- [MAVEN_HOME](http://maven.apache.org/download.cgi)
  - bin
    - mvn
  - boot
  - conf
    - settings.xml
  - lib

### 环境变量

```batch
REM 首先确保JAVA_HOME已配置完成

REM 添加系统环境变量MAVEN_HOME
SET MAVEN_HOME=...

REM 添加到系统环境变量PATH
SET PATH=%PATH%;%MAVEN_HOME%\bin

REM 测试环境
mvn -v
```

```txt
Apache Maven ?.?.?
Maven home: ...
Java version: ?.?.?, vendor: Oracle Corporation, runtime: ...\jre
Default locale: zh_CN, platform encoding: GBK
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
```

### 仓库类型

>可以通过修改`%MAVEN_HOME%\conf\settings.xml`修改相关配置。

- 本地仓库：默认位于`%UserProfile%\.m2\repository`
- 中央仓库：放置了所有开源jar包
- 远程仓库：私服仓库

#### 配置本地仓库

```xml
<settings>

  <!-- ... -->

  <localRepository>${user.home}/.m2/repository</localRepository>

  <!-- ... -->
```

#### 配置中央仓库

```xml
<settings>

  <!-- ... -->

  <mirrors>

    <!-- ... -->

    <!-- 阿里云仓库 -->
    <mirror>
      <id>alimaven</id>
      <name>AliyunMaven</name>
  　　<url>https://maven.aliyun.com/repository/public</url>
      <mirrorOf>central</mirrorOf>
    </mirror>

    <!-- ... -->
  
  </mirrors>

  <!-- ... -->
```

## 项目标准目录结构

- src
  - main
    - java: 核心代码
    - resources: 配置文件
    - webapp: 页面资源
  - test
    - java: 测试代码
    - resources: 测试配置文件
  - pom.xml: mvn项目配置信息
  - target: 编译和打包存储目录

### pom.xml

```xml
<project>

    <!-- 模型版本 -->
    <modelVersion>4.0.0</modelVersion>

    <!-- 组织的唯一ID -->
    <groupId>org.example</groupId>

    <!-- 项目的唯一ID，一个groupId下面可能多个项目，靠artifactId来区分 -->
    <artifactId>HelloMaven</artifactId>

    <!-- 项目名称 -->
    <name>HelloMaven</name>

    <!-- 版本号 -->
    <version>1.0-SNAPSHOT</version>

    <!-- 打包格式 -->
    <packaging>jar</packaging>

    <!-- 引入外部依赖 -->
    <dependencies>
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
      </dependency>
    </dependencies>

    <!-- ... -->
  
</project>
```

## 生命周期

### 清理生命周期

```batch
REM 删除编译的结果
mvn clean
```

### 默认生命周期

```batch
REM 删除编译的结果
mvn clean

REM 编译src/main/java到target目录下
mvn compile

REM 编译src/test/java到target目录下
mvn test

REM 打包项目到target目录下
mvn package

REM 打包项目到本地仓库
mvn install

REM 打包项目到私服
mvn deploy
```

### 站点生命周期

略

## 创建项目

- `-DgourpId`: 组织名
- `-DartifactId`: 项目名
- `-DarchetypeArtifactId`: 模板类型
- `-DinteractiveMode`: 是否使用交互模式

```batch
REM 创建
mvn archetype:generate "-DgroupId=com.zhmh" "-DartifactId=HelloMaven" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"

REM 编译
mvn clean compile

REM 执行
java -cp "target/classes" com.zhmh.App
```

## IDEA配置

配置本地maven位置

- ![mi1](images/maven_idea_1.png)

解决不联网无法创建maven工程的问题

- ![mi2](images/maven_idea_2.png)

```txt
-DarchetypeCatalog=internal
```