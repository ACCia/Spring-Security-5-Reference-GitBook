## 2.1什么是Spring Security？

Spring Security为基于Java EE的企业软件应用程序提供全面的安全服务。特别强调支持使用Spring Framework构建的项目，Spring Framework是面向企业软件开发的领先Java EE解决方案。如果您不使用Spring来开发企业应用程序，我们热烈鼓励您仔细观察。熟悉Spring（特别是依赖注入原则）可以帮助您更轻松地加快Spring Security的速度。

人们使用Spring Security有很多原因，但是大部分都是在找到Java EE的Servlet规范或EJB规范的安全特性之后才被吸引到项目中，缺乏典型的企业应用场景所需的深度。虽然提到这些标准，但重要的是要认识到它们在WAR或EAR级别不可移植。因此，如果您切换服务器环境，则在新的目标环境中重新配置应用程序的安全性通常需要大量工作。使用Spring Security克服了这些问题，并为您带来了数十种其他有用的，可定制的安全功能。

你可能知道应用安全的两个主要领域是“认证”和“授权”（或“访问控制”）。这些是Spring Security目标的两个主要领域。“认证”是建立主体的过程，即他们所声称的（“主体”通常是指可以在您的应用程序中执行操作的用户，设备或其他系统）“授权”是指决定的过程是否允许委托人在您的申请中执行行动。为了到达需要授权决定的地方，认证过程已经建立了委托人的身份。这些概念是常见的，而不是Spring Security所有。

在认证级别，Spring Security支持各种认证模型。这些认证模型中的大多数由第三方提供，或者由互联网工程任务组等相关标准机构开发。此外，Spring Security提供了自己的身份验证功能。具体来说，Spring Security目前支持与所有这些技术的认证集成：

* HTTP BASIC认证头（基于IETF RFC的标准）
* HTTP摘要认证标头（基于IETF RFC的标准）
* HTTP X.509客户端证书交换（基于IETF RFC的标准）
* LDAP（一种非常常见的跨平台身份验证方法，特别是在大型环境中）
* 基于表单的身份验证（用于简单的用户界面需求）
* OpenID身份验证
* 基于预先建立的请求头（例如Computer Associates Siteminder）进行身份验证
* Jasig中央认证服务（也称为CAS，这是一个流行的开源单点登录系统）
* 远程方法调用（RMI）和HttpInvoker（Spring远程处理协议）的透明身份验证上下文传播
* 自动“记住我”身份验证（所以您可以勾选一个框以避免在一段预定时间内重新认证）
* 匿名认证（允许每个未认证的呼叫自动承担特定的安全身份）
* 运行身份验证（如果一个呼叫应该继续使用不同的安全身份，这是非常有用的）
* Java认证和授权服务（JAAS）
* Java EE容器认证（所以如果需要，您仍然可以使用容器管理身份验证）
* Kerberos的
* Java开源单点登录（JOSSO）\*
* OpenNMS网络管理平台\*
* AppFuse \*
* AndroMDA \*
* 骡子ESB \*
* 直接Web请求（DWR）\*
* Grails \*
* 挂毯\*
* JTrac \*
* Jasypt \*
* 滚筒 \*
* 弹性路径\*
* 阿特兰克人\*
* 您自己的认证系统（见下文）

（\*表示由第三方提供

许多独立软件供应商（ISV）采用Spring Security，因为这种灵活的认证模式是非常重要的选择。这样做可以使他们能够快速地将他们的解决方案与终端客户需要的解决方案结合起来，而不需要进行大量的工程设计或者要求客户改变他们的环境。如果上述认证机制都不符合您的需求，Spring Security就是一个开放平台，编写自己的认证机制很简单。Spring Security的许多企业用户需要与不遵循任何特定安全标准的“遗留”系统集成，Spring Security很乐意与这样的系统“玩得很好”。

不管认证机制如何，Spring Security提供了一套深度的授权功能。有三个主要的兴趣领域：授权Web请求，授权是否可以调用方法并授权访问各个域对象实例。为了帮助您了解差异，请分别考虑Servlet规范Web模式安全性，EJB容器管理安全性和文件系统安全性中的授权功能。Spring Security在所有这些重要领域提供了深刻的功能，我们将在本参考指南中进一步探讨。



## 2.2历史

Spring Security began in late 2003 as "The Acegi Security System for Spring". A question was posed on the Spring Developers' mailing list asking whether there had been any consideration given to a Spring-based security implementation. At the time the Spring community was relatively small \(especially compared with the size today!\), and indeed Spring itself had only existed as a SourceForge project from early 2003. The response to the question was that it was a worthwhile area, although a lack of time currently prevented its exploration.

考虑到这一点，构建了一个简单的安全实现，而不是发布。几周后，Spring社区的另一位成员询问了安全性，当时提供了这个代码。另外还有其他一些请求，到2004年1月，大约二十人正在使用这些代码。这些开创性的用户被其他人加入，他们建议SourceForge项目顺利进行，该项目于2004年3月正式成立。

在这些早期，该项目没有任何自己的认证模块。集装箱管理安全性依赖于身份验证过程，而Acegi Security则侧重于授权。首先这是合适的，但随着越来越多的用户要求额外的容器支持，容器特定认证领域接口的基本限制变得清晰。还有一个相关的问题是向容器的类路径添加新的JAR，这是最终用户混淆和配置错误的常见来源。

随后引入了Acegi安全认证服务。大约一年后，Acegi Security成为Spring Framework的一个官方子项目。1.0.0的最终版本于2006年5月发布，经过两年半以上的积极使用，在众多的生产软件项目和数百个改进和社区的贡献。

Acegi Security于2007年底成为官方的Spring Portfolio项目，并被重新命名为“Spring Security”。

今天，Spring Security拥有强大而活跃的开源社区。在支持论坛上有关于Spring Security的成千上万的消息。开发人员的活跃核心是代码本身和一个活跃的社区，这些社区也定期分享补丁并支持同行。



## 2.3版本编号

了解Spring Security版本号码的工作原理是有用的，因为这将有助于您识别迁移到未来版本的项目所涉及的工作（或缺乏）。每个版本都使用标准的三元组整数：MAJOR.MINOR.PATCH。意图是MAJOR版本是不兼容的，大规模升级的API。MINOR版本应该在很大程度上保留与较旧的次要版本的源和二进制兼容性，认为可能有一些设计更改和不兼容的更新。PATCH级别应该是完美兼容的，向前和向后，可能的例外是修复错误和缺陷的更改。

您受到更改影响的程度将取决于代码的集成程度。如果您正在做很多自定义，那么您比使用简单的命名空间配置更有可能受到影响。

您应该总是先测试您的应用程序，然后再推出新版本。

## 2.4获取Spring安全性

您可以通过几种方式掌握Spring Security。您可以从主要的[Spring Security](https://spring.io/spring-security)页面下载一个打包的发行版，从Maven Central存储库中下载单个jar（或者一个用于快照和里程碑版本的Spring Maven存储库），或者您可以从源代码自行构建项目。

### 2.4.1使用Maven

一个最小的Spring Security Maven依赖关系通常如下所示：

**pom.xml中。 **

```
<
依赖关系
>
<
！ -  ...其他依赖元素...  - 
>
<
dependency
>
<
groupId
>
 org.springframework.security 
<
/ groupId
>
<
artifactId
>
 spring-security-web 
<
/ artifactId
>
<
version
>
 5.0 .0.M3 
<
/ version
>
<
/ dependency
>
<
dependency
>
<
groupId
>
 org.springframework.security 
<
/ groupId
>
<
artifactId
>
 spring-security-config 
<
/ artifactId
>
<
version
>
 5.0.0.M3 
<
/ version 
>
<
/ dependency
>
<
/ dependencies
>
```



如果您正在使用其他功能（如LDAP，OpenID等），则还需要包含相应的[第2.4.3节“项目模块”](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/#modules)。

#### Maven存储库

所有GA版本（即以.RELEASE结尾的版本）都部署到Maven Central，因此您的pom中不需要声明其他Maven存储库。

如果您使用SNAPSHOT版本，则需要确保Spring Snapshot存储库的定义如下所示：

**pom.xml中。 **

```
<
repository
>
<
！ - 可能是其他存储库元素...  - 
>
<
repository
>
<
id
>
 spring-snapshot 
<
/ id
>
<
name
>
 Spring Snapshot Repository 
<
/ name
>
<
url
>
 http：// repo.spring.io/snapshot 
<
/ url
>
<
/ repository
>
<
/ repositories
>
```



如果您使用里程碑或版本候选版本，则需要确保Spring Milestone存储库的定义如下所示：

**pom.xml中。 **

```
<
repository
>
<
！ - 可能是其他存储库元素...  - 
>
<
repository
>
<
id
>
 spring-milestone 
<
/ id
>
<
name
>
 Spring里程碑存储库
<
/ name
>
<
url
>
 http：// repo.spring.io/milestone 
<
/ url
>
<
/ repository
>
<
/ repositories
>
```



#### Spring框架Bom

Spring Security针对Spring Framework 5.0.0.RC3构建，但应该与4.0.x一起工作。许多用户将会遇到的问题是，Spring Security的传递性依赖关系解决了Spring Framework 5.0.0.RC3，这可能会导致奇怪的类路径问题。

一个（乏味）的方式来规避这个问题将是将所有的Spring框架模块包含在你的pom的[&lt;dependencyManagement&gt;](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Dependency_Management)部分。另一种方法是将`spring-framework-bom`您的`<dependencyManagement>`部分中`pom.xml`包含如下所示：

**pom.xml中。 **

```
<
dependencyManager
>
<
dependencies
>
<
dependency
>
<
groupId
>
 org.springframework 
<
/ groupId
>
<
artifactId
>
 spring-framework-bom 
<
/ artifactId
>
<
version
>
 5.0.0.RC3 
<
/ version
>
<
type
>
 pom 
<
/ type 
>
<
scope
>
 import 
<
/ scope
>
<
/ dependency
>
<
/ dependencies
>
<
/ dependencyManagement
>
```



这将确保Spring Security的所有传递依赖使用Spring 5.0.0.RC3模块。

| ![](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/images/note.png "\[注意\]") |
| :--- |
| 这种方法使用Maven的“物料清单”（BOM）概念，仅在Maven 2.0.9+中可用。有关如何解决依赖关系的更多详细信息，请参考[Maven的“依赖机制简介”文档](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)。 |

### 2.4.2毕业

一个最小的Spring Security Gradle依赖关系通常如下所示：

**的build.gradle。 **

```
依赖{

	编译
'org.springframework.security:spring-security-web:5.0.0.M3'
 
	编译
'org.springframework.security:spring-security-config:5.0.0.M3'
 
}
```



如果您正在使用其他功能（如LDAP，OpenID等），则还需要包含相应的[第2.4.3节“项目模块”](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/#modules)。

#### 毕业资料库

所有GA版本（即以.RELEASE结尾的版本）都部署到Maven Central，因此使用mavenCentral（）存储库对于GA版本是足够的。

**的build.gradle。 **

```
存储库{

	mavenCentral（）

}
```



如果您使用SNAPSHOT版本，则需要确保Spring Snapshot存储库的定义如下所示：

**的build.gradle。 **

```
存储库{

	maven {url'https 
://repo.spring.io/snapshot'
 }

}
```



如果您使用里程碑或版本候选版本，则需要确保Spring Milestone存储库的定义如下所示：

**的build.gradle。 **

```
存储库{

	maven {url'https 
://repo.spring.io/milestone'
 }

}
```



#### 使用Spring 4.0.x和Gradle

默认情况下，Gradle将在解析传递版本时使用最新版本。这意味着在使用Spring Framework 5.0.0.RC3运行Spring Security 5.0.0.M3时通常不需要额外的工作。然而，有时可能会出现问题，所以最好使用[Gradle的ResolutionStrategy](http://www.gradle.org/docs/current/dsl/org.gradle.api.artifacts.ResolutionStrategy.html)来减轻这个问题，如下所示：

**的build.gradle。 **

```
configured.all {

	resolutionStrategy.eachDependency {DependencyResolveDetails details  - 
>
if
（details.requested.group == 
'org.springframework'
）{

			details.useVersion'5.0.0.RC3 
'

		}

	}

}
```



这将确保Spring Security的所有传递依赖使用Spring 5.0.0.RC3模块。

| ![](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/images/note.png "\[注意\]") |
| :--- |
| 此示例使用Gradle 1.9，但是可能需要修改才能在Gradle的未来版本中工作，因为这是Gradle中的一个孵化功能。 |

### 2.4.3项目模块

在Spring Security 3.0中，代码库已被细分为单独的jar，它们更清楚地区分不同的功能区域和第三方依赖关系。如果您使用Maven构建项目，那么这些是您将添加到您的项目的模块`pom.xml`。即使您不使用Maven，我们建议您查看`pom.xml`文件以了解第三方依赖关系和版本。或者，一个好主意是检查示例应用程序中包含的库。

#### 核心 - spring-security-core.jar

包含核心认证和访问轮廓类和接口，远程支持和基本配置API。使用Spring Security的任何应用程序都需要。支持独立应用程序，远程客户端，方法（服务层）安全性和JDBC用户配置。包含顶层软件包：

* `org.springframework.security.core`
* `org.springframework.security.access`
* `org.springframework.security.authentication`
* `org.springframework.security.provisioning`

#### Remoting - spring-security-remoting.jar

提供与Spring Remoting的集成。除非您正在编写一个使用Spring Remoting的远程客户端，否则您不需要这样做。主要包装是`org.springframework.security.remoting`。

#### Web - spring-security-web.jar

包含过滤器和相关的Web安全基础设施代码。任何与servlet API依赖关系。如果您需要Spring Security Web认证服务和基于URL的访问控制，您将需要它。主要包装是`org.springframework.security.web`。

#### Config - spring-security-config.jar

包含安全命名空间解析代码和Java配置代码。如果您使用Spring Security XML命名空间进行配置或Spring Security的Java配置支持，则需要它。主要包装是`org.springframework.security.config`。没有一个类用于在应用程序中直接使用。

#### LDAP - spring-security-ldap.jar

LDAP认证和配置代码。如果需要使用LDAP认证或管理LDAP用户条目，则必需。顶级包是`org.springframework.security.ldap`。

#### ACL - spring-security-acl.jar

专用域对象ACL实现。用于将安全性应用于应用程序中的特定域对象实例。顶级包是`org.springframework.security.acls`。

#### CAS - spring-security-cas.jar

Spring Security的CAS客户端集成。如果要使用Spring Security Web认证与CAS单点登录服务器。顶级包是`org.springframework.security.cas`。

#### OpenID - spring-security-openid.jar

OpenID Web认证支持。用于对外部OpenID服务器进行身份验证。`org.springframework.security.openid`。需要OpenID4Java。

#### 测试 - spring-security-test.jar

支持使用Spring Security进行测试。

### 2.4.4检查源

由于Spring Security是一个开源项目，我们强烈建议您使用git查看源代码。这将使您可以完全访问所有示例应用程序，您可以轻松地构建项目的最新版本。拥有项目的来源也是调试的巨大帮助。异常堆栈跟踪不再是黑盒子的问题，但您可以直接了解导致问题的线路，并解决发生了什么。来源是项目的最终文档，通常是查找实际工作原理的最简单的地方。

要获取项目的源，请使用以下git命令：

```
git clone https://github.com/spring-projects/spring-security.git
```

这将允许您访问本地计算机上的整个项目历史记录（包括所有版本和分支）。

