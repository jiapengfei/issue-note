# Spring Boot

## [Spring Boot Executable Jar with Classpath(loader.path)](https://stackoverflow.com/questions/39716796/spring-boot-executable-jar-with-classpath)

## [Spring Boot 用gradle bootJar打包瘦身(外置依赖jar)](https://my.oschina.net/formatkm/blog/1822900)

## [Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/html/)

## @ConfigurationProperties

    把yml配置文件中的属性映射成Java对象时，需要设置对应属性的get，set方法

## @注解修饰List,Map集合
    @Autowired @Bean 把泛型的所有对象实例放入集合，Map的key是对象实例的name

## BeanDefinitionRegistryPostProcessor和BeanPostProcessor接口
    自定义处理Spring Bean的定义和创建Bean的行为

[spring boot(五)：spring data jpa的使用](https://www.cnblogs.com/ityouknow/p/5891443.html)

[Spring缓存注解@Cacheable、@CacheEvict、@CachePut使用](https://www.cnblogs.com/fashflying/p/6908028.html)
     
     默认的key生成策略是通过KeyGenerator生成的，其默认策略如下：
     如果方法没有参数，则使用0作为key。
     如果只有一个参数的话则使用该参数作为key。
     如果参数多余一个的话则使用所有参数的hashCode作为key。

[@RequestParam @RequestBody @PathVariable 等参数绑定注解详解](https://www.cnblogs.com/guoyinli/p/7056146.html)
