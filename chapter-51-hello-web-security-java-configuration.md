* 通过\`@EnableWebSecurity\` 创建Spring Security Java 配置
* 该配置创建一个Servlet过滤器\`springSecurityFilterChain\`, 负责所有的安全性

示例 ：

```
import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.context.annotation。*;
import org.springframework.security.config.annotation.authentication.builders。*;
import org.springframework.security.config.annotation.web.configuration。*;

@EnableWebSecurity
 public  class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Bean
     public UserDetailsS​​ervice userDetailsS​​ervice（） throws Exception {
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager（）;
        manager.createUser（User.withUsername（“user”）. password（“password”）.roles（“USER”）.build（））;
        退货经理
    }
}
```

包括功能如：

需要验证您应用程序中的每个URL

* 为您生成登录表单
* 允许具有**用户名**_用户_和**密码**_密码_的用户使用基于表单的身份验证进行身份验证
* 允许用户注销
* [CSRF攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)预防
* [会话固定](https://en.wikipedia.org/wiki/Session_fixation)保护
* 安全头集成

  * [HTTP严格传输安全性](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) 用于安全请求
  * [X-Content-Type-Options](https://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx)
    集成
  * 缓存控制（可以稍后被应用程序覆盖以允许缓存静态资源）
  * [X-XSS保护](https://msdn.microsoft.com/en-us/library/dd565647%28v=vs.85%29.aspx)
    集成
  * X-Frame-Options集成，以防止
    [Clickjacking](https://en.wikipedia.org/wiki/Clickjacking)

* 与以下Servlet API方法集成

  * [HttpServletRequest的＃getRemoteUser（）](https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html#getRemoteUser%28%29)
  * [HttpServletRequest.html＃getUserPrincipal（）](https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html#getUserPrincipal%28%29)
  * [HttpServletRequest.html＃的isUserInRole（java.lang.String中）](https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html#isUserInRole%28java.lang.String%29)
  * [HttpServletRequest.html＃login（java.lang.String，java.lang.String）](https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html#login%28java.lang.String, java.lang.String%29)
  * [HttpServletRequest.html＃注销（）](https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html#logout%28%29)

### 5.1.1 AbstractSecurityWebApplicationInitializer

下一步是注册`springSecurityFilterChain`战争。这可以在Servlet 3.0+环境中使用[Spring的WebApplicationInitializer支持的](http://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/mvc.html#mvc-container-config)Java配置中完成。不要惊讶，Spring Security提供了一个基础类`AbstractSecurityWebApplicationInitializer`，可以确保`springSecurityFilterChain`为您注册。我们使用的方式`AbstractSecurityWebApplicationInitializer`取决于我们是否已经在使用Spring，或者Spring Security是我们应用程序中唯一的Spring组件。

* [第5.1.2节“AbstractSecurityWebApplicationInitializer without Existing Spring”](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/#abstractsecuritywebapplicationinitializer-without-existing-spring)
  - 如果您没有使用Spring，请使用这些说明
* [第5.1.3节“AbstractSecurityWebApplicationInitializer with Spring MVC”](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/#abstractsecuritywebapplicationinitializer-with-spring-mvc)
  - 如果您已经在使用Spring，请使用这些说明

### 5.1.2 AbstractSecurityWebApplicationInitializer没有现有的Spring

如果您不使用Spring或Spring MVC，则需要将其`WebSecurityConfig`传入超类，以确保配置被拾取。你可以在下面找到一个例子：

```
import org.springframework.security.web.context.*;

public class SecurityWebApplicationInitializer
	extends AbstractSecurityWebApplicationInitializer {

	public SecurityWebApplicationInitializer() {
		super(WebSecurityConfig.class);
	}
}
```

该`SecurityWebApplicationInitializer`会做以下事情：

* 为应用程序中的每个URL自动注册springSecurityFilterChain过滤器
* 添加加载
  [WebSecurityConfig](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/#jc-hello-wsca)
  的ContextLoaderListener
  。



