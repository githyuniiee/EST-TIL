## 시큐리티 설정하기

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityCustomizer;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;

import static org.springframework.boot.autoconfigure.security.servlet.PathRequest.toH2Console;

@EnableWebSecurity
@Configuration
public class WebSecurityConfig {
    private UserDetailService userDetailService;

    public WebSecurityConfig(UserDetailService userDetailService) {
        this.userDetailService = userDetailService;
    }

    @Bean
    public WebSecurityCustomizer configure() {      // 1) 스프링 시큐리티 기능 비활성화, 인증/인가 모든 곳에 적용 X
        return web -> web.ignoring().requestMatchers(toH2Console())
                .requestMatchers("/static/**");
    }

    // 2) 특정 HTTP 요청에 대한 웹 기반 보안 구성
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity httpSecurity) throws Exception {
        return httpSecurity.authorizeHttpRequests()    // 3) 인증, 인가 설정
                .requestMatchers("/login", "/signup", "/user").permitAll() //url access 설정
                .anyRequest().authenticated() // 이외 url 요청 설정
                .and()
                .formLogin()        //4) 폼 기반 로그인 설정
                .loginPage("/login") //로그인 페이지 경로 설정
                .defaultSuccessUrl("/articles") //로그인 완료되었을 때 이동할 경로 설정
                .and()
                .logout()       // 5) 로그아웃 설정
                .logoutSuccessUrl("/login") //로그아웃 완료되었을 때 이동할 경로 설정
                .invalidateHttpSession(true) //로그아웃 이후에 세션을 삭제할지 여부 설정
                .and()
                .csrf().disable()       // 6) csrf 비활성화
                .build();
    }

    // 7) 인증관리자 관련 설정
    @Bean
    public AuthenticationManager authenticationManager(HttpSecurity httpSecurity, BCryptPasswordEncoder bCryptPasswordEncoder, UserDetailService userDetailService) {
        return httpSecurity.getSharedObject(AuthenticationManagerBuilder.class)
                .userDetailsService(userDetailService)  // 8) 사용자 정보 서비스 설정
                .passwordEncoder(bCryptPasswordEncoder)
                .and()
                .build();
    }
    
    // 9) 패스워드 인코더로 사용할 빈 등록 
    @Bean
    public BCryptPasswordEncoder bCryptPasswordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

<br></br>
## CSRF (**Cross-Site Request Forgery)**

- 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위를 특정 웹사이트에 요청하게 하는 공격
- 
<br></br>
## 스프링 시큐리티 정리

인증 : `등록된 사용자의 신원을 입증하는 과정`

인가 : 특정 부분에 `접근할 수 있는지를 확인하는 과정`

- 각 필터에서 인증, 인가와 관련된 작업을 처리합니다. 기본적으로 세션&쿠키 방식으로 인증을 처리
    - 스프링 시큐리티에서 사용자의 인증, 인가 정보를 UserDetails 객체에 담음
    - 스프링 시큐리티에서 사용자의 정보를 가져오는 데 사용하는 UserDetailService를 사용 이 클래스를 상속받은 뒤 loadUserByUsername()을 오버라이드하면 스프링 시큐리티에서 사용자의 정보를 가져올 때 오버라이드된 메소드를 사용
