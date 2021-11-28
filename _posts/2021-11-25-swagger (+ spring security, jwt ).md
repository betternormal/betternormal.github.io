---
layout: post
title: "swagger (+ spring security, jwt )"
author: "praconfi"
tags: web spring
---

# swagger (+ spring security, jwt )

잘 사용중이던 swager가 갑자기 화이트 에러페이지를 보이기 시작했다.

서버에 spring security를 적용하고, jwt방식으로 인증을 구현했는데 ,swagger url 접속 시 토큰이 없어 생긴 문제였다(401 Unauthorized) 아래의 순서로 해결했다.

![스크린샷 2021-11-16 15 59 17](https://user-images.githubusercontent.com/64571546/143409069-e7c61982-7605-4b59-863c-5692c95b3a93.png)

## 1. Spring security에서 해당 url을 무시하도록 설정한다

```java
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    private final TokenProvider tokenProvider;
    private final JwtAuthenticationEntryPoint jwtAuthenticationEntryPoint;
    private final JwtAccessDeniedHandler jwtAccessDeniedHandler;

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    // Spring security룰을 무시하게 하는 url규칙
    @Override
    public void configure(WebSecurity web) {
        web.ignoring()
                .antMatchers("/h2-console/**", "/favicon.ico")
                .antMatchers("/v2/api-docs", "/swagger-resources/**", "/swagger-ui.html", "/webjars/**", "/swagger/**");
//                .antMatchers("/resources/**")
//                .antMatchers("/css/**")
//                .antMatchers("/vendor/**")
//                .antMatchers("/js/**")
//                .antMatchers("/favicon*/**")
//                .antMatchers("/img/**")
    }

    // Spring security 규칙
    @Override
    protected void configure(HttpSecurity http) throws Exception {

        http.authorizeRequests() // 권한요청 처리 설정 메서드
                .antMatchers( "/h2-console/**" ).permitAll() // 누구나 h2-console 접속 허용
                .and() // ...
                .csrf().ignoringAntMatchers( "/h2-console/**" ).disable(); // GET메소드는 문제가 없는데 POST메소드만 안되서 CSRF 비활성화 시킴

        // CSRF 설정 Disable
        http.csrf().disable()

                // exception handling 할 때 우리가 만든 클래스를 추가
                .exceptionHandling()
                .authenticationEntryPoint(jwtAuthenticationEntryPoint)
                .accessDeniedHandler(jwtAccessDeniedHandler)

                // h2-console 을 위한 설정을 추가
                .and()
                .headers()
                .frameOptions()
                .sameOrigin()

                // 시큐리티는 기본적으로 세션을 사용
                // 여기서는 세션을 사용하지 않기 때문에 세션 설정을 Stateless 로 설정
                .and()
                .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)

                // 로그인, 회원가입 API 는 토큰이 없는 상태에서 요청이 들어오기 때문에 permitAll 설정
                .and()
                .authorizeRequests()
                .antMatchers("/api/trade-talk/auth/**").permitAll()
                .anyRequest().authenticated()   // 나머지 API 는 전부 인증 필요

                // JwtFilter 를 addFilterBefore 로 등록했던 JwtSecurityConfig 클래스를 적용
                .and()
                .apply(new JwtSecurityConfig(tokenProvider));

    }
}
```

## 2. swagger UI에  authorize기능을 추가한다(API 요청을 보낼때 헤더에 토큰을 자동으로 실어준다, **Swagger 2.9.2부터 지원**)

![스크린샷 2021-11-17 10 11 47](https://user-images.githubusercontent.com/64571546/143409146-106c639f-3b90-48b6-8976-a0fdcdd1b354.png)

토큰이 없어 swagger로 API요청시 401에러발생

```java
// tradeTalk/src/main/java/com/loginnw/tradetalk/config/Swagger2Config.java

package com.loginnw.tradetalk.config;
import com.google.common.collect.Lists;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpHeaders;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.ParameterBuilder;

import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.schema.ModelRef;
import springfox.documentation.service.*;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spi.service.contexts.SecurityContext;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

@Configuration
@EnableSwagger2
public class Swagger2Config {

    private static final String API_NAME = "Trade Talk API";
    private static final String API_VERSION = "1.0";
    private static final String API_DESCRIPTION = "Trade Talk 서버 API 문서";

    @Bean
    public Docket api() {

        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo()) // API 문서에 대한 내용
                .securityContexts(Arrays.asList(securityContext())) // swagger에서 jwt 토큰값 넣기위한 설정
                .securitySchemes(Arrays.asList(apiKey())) // swagger에서 jwt 토큰값 넣기위한 설정
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.loginnw.tradetalk")) // Swagger를 적용할 package명 작성
                .paths(PathSelectors.any()) // PathSelectors.any() 해당패키지 하위에 있는 모든 url에 적용, 특정 url만 선택 가능
                .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title(API_NAME) // API 이름지정
                .version(API_VERSION) // API 버전
                .description(API_DESCRIPTION) // API 설명
                //.license("라이센스 작성")
                //.licenseUrl("라이센스 URL 작성")
                .build();
    }

    // swagger에서 jwt 토큰값 넣기위한 설정
    private ApiKey apiKey() {
        return new ApiKey("JWT", "Authorization", "header");
    }

    private SecurityContext securityContext() {
        return SecurityContext.builder().securityReferences(defaultAuth()).build();
    }

    private List<SecurityReference> defaultAuth() {
        AuthorizationScope authorizationScope = new AuthorizationScope("global", "accessEverything");
        AuthorizationScope[] authorizationScopes = new AuthorizationScope[1];
        authorizationScopes[0] = authorizationScope;
        return Arrays.asList(new SecurityReference("JWT", authorizationScopes));
    }
}
```

![Untitled](https://user-images.githubusercontent.com/64571546/143409205-670d9581-35cf-4c25-8dda-1af5c276fa14.png)

설정이 완료되면 오른쪽에 인증버튼이 생긴다. 

![스크린샷 2021-11-17 16 20 10](https://user-images.githubusercontent.com/64571546/143409261-f25d9cea-fa5f-4b69-a992-c4d869be8333.png)

토큰값을 입력해주면 다른 API요청시 헤더에 첨부되어 전송된다.
