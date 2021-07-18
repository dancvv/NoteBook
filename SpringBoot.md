# SpringBoot

## 集成JDBC

引入启动器和驱动

````java
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
<dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
</dependency>
````

编写配置文件

```java
spring:
  datasource:
    username: root
    data-password: 13476110270dwx
    url: jdbc:mysql://localhost:3306/springboot?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    driver-class-name: com.mysql.cj.jdbc.Driver
```



测试

```java
@Test
    void testData() throws SQLException {
        //查看数据源类型
        System.out.println(dataSource.getClass());
        //获取连接
        Connection connection=dataSource.getConnection();
        System.out.println(connection);
        //关闭连接
        connection.close();
    }
```

### 1. 数据源的自动配置

数据库驱动?

官方不导入驱动

官方已经对版本号进行了仲裁，数据库版本和驱动版本对应



**JAVA 可以静态导入包，直接使用方法，而不用创建对象**

