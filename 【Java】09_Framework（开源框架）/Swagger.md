> 当前位置：【Java】09_Framework（开源框架）-> Swagger



## 1、swagger 地址

- 官网：https://swagger.io/
- Swagger-Bootstrap-UI / knife4j 使用文档：https://doc.xiaominfo.com/knife4j/
- Swagger-Bootstrap-UI / knife4j 代码：https://github.com/xiaoymin/swagger-bootstrap-ui



## 2、Swagger-Bootstrap-UI 使用

### 步骤1：pom.xml 添加依赖包

```xml
<!--Swagger2-->
<!--访问路径：http://localhost:端口号/swagger-ui.html-->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>

<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>

<!-- swagger图形化接口 -->
<!--访问路径：http://localhost:端口号/doc.html-->
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>swagger-bootstrap-ui</artifactId>
    <version>1.9.6</version>
</dependency>

<!-- 两个配置解决 NumberFormatException -->
<dependency>
    <groupId>io.swagger</groupId>
    <artifactId>swagger-annotations</artifactId>
    <version>1.5.22</version>
</dependency>

<dependency>
    <groupId>io.swagger</groupId>
    <artifactId>swagger-models</artifactId>
    <version>1.5.22</version>
</dependency>
```

### 步骤2：添加 SwaggerConfig.java

```java
package com.loto.config;

import com.github.xiaoymin.swaggerbootstrapui.annotations.EnableSwaggerBootstrapUI;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2 //开启Swagger
@EnableSwaggerBootstrapUI
public class SwaggerConfig {
    // http://localhost:6085/mail/doc.html
    // 配置swagger2核心配置
    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2) // 指定api类型位swagger2
                .apiInfo(apiInfo())                    // 用于定义api文档汇总信息
                .select().apis(RequestHandlerSelectors.basePackage("com.loto.xxx")) // 指定生成文档的 controller
                .paths(PathSelectors.any())
                .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("xxxx接口api") // 文档标题
                .contact(new Contact("", // 作者
                        "",  // URL
                        "")) // email
                .description("xxxl接口api")           // 详细信息
                .version("1.0.0")                    // 文档版本号
                .termsOfServiceUrl("")               // 网站地址
                .build();
    }
}
```





## 3、knife4j 使用