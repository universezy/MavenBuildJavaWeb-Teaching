# MavenBuildJavaWeb-Teaching

## 前言

本文使用Ubuntu16.04LTS操作系统+Eclipse集成开发环境+Tomcat服务器，通过Maven构建Java Web工程。

---
## 一、 配置Maven

参考我的另一篇文章[Ubuntu下Maven的配置](https://blog.csdn.net/zy13608089849/article/details/79725469)

---
## 二、 配置Tomcat

参考我的另一篇文章[Ubuntu下搭建Tomcat服务器](https://blog.csdn.net/zy13608089849/article/details/79730550)

---
## 三、 将Maven添加到Eclipse

### 1.

菜单栏：Window - Preferences - Maven - Installations - Add，添加Maven目录

![](image/13.png?raw=true)

### 2.

左边导航栏切换到User Settings - Global Settings - Browse

进入Maven目录 - conf，选择settings.xml文件

Update Settings - Apply

![](image/14.png?raw=true)

---
## 四、 新建Tomcat服务器

菜单栏：Window - Preferences - Server - Environment - Add - 添加Tomcat服务器

![](image/11.png?raw=true)

设置Tomcat目录

![](image/12.png?raw=true)

---
## 五、 新建Maven工程

### 1.

菜单栏：File - New - Other - Maven - Maven Project - Next

![](image/01.png?raw=true)

### 2.

"Select project name and location"页不管，next

### 3.

"Select an Archetype"页，选择webapp，next

![](image/02.png?raw=true)

### 4.

输入Group Id企业名和Artifact Id项目名，finish

![](image/03.png?raw=true)

---
## 六、 修改工程

### 1.

也可参考[Java Web工程中index.jsp报"javax.servlet.http.HttpServlet"错误的解决方案 ](https://blog.csdn.net/zy13608089849/article/details/79814219)解决。

此时工程有报错感叹号，定位在index.jsp文件，出现这个错误是因为缺少Servlet包，前往Maven仓库搜索[Servlet](http://mvnrepository.com/artifact/javax.servlet/servlet-api)，然后在pom.xml文件中添加依赖，参考：
```xml
<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>servlet-api</artifactId>
	<version>2.5</version>
	<scope>provided</scope>
</dependency>
```

![](image/04.png?raw=true)

如果不行，工程右键 - Build Path - Configure Build Path

右边顶部导航栏选择Libraries - 右边Add Library - Server Runtime - 选择Tomcat服务器 - Apply

![](image/05.png?raw=true)

### 2.

Java Resources文件夹下应该有这四个文件夹：

- scr/main/java
- scr/main/resources
- scr/test/java
- scr/test/resources

![](image/06.png?raw=true)

如果有缺失，Java Resources右键 - New - Source Folder，按照相对路径创建文件夹

如果创建时提示已存在无法创建，就工程右键 - Refresh，看有没有出现

如果还是没有，就去工程目录下手动建

![](image/07.png?raw=true)

工程右键 - Build Path - Configure Build Path

右边顶部导航栏选择Source

![](image/08.png?raw=true)

上面四个文件夹，两个main的Output folder是target/classes，两个test的Output folder是target/test-classes，如果不对，点击对应项，Edit里修改

![](image/09.png?raw=true)

### 3.

开始编写web工程

pom.xml文件中按需添加工程所需jar包的依赖，资源均来自[Maven仓库](http://mvnrepository.com/)

---
## 七、 启动Tomcat服务器

确保web.xml文件配置正确的情况下

工程右键 - Run As - Run on Server

![](image/10.png?raw=true)


