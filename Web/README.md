### Web配置

#### Cookie
```java
// 禁止将sessionId写入到URL后缀中
@Bean
public ServletContextInitializer servletContextInitializer() {
	return servletContext -> servletContext.setSessionTrackingModes(Collections.singleon(SessionTrackingModes.COOKIE));
}
```