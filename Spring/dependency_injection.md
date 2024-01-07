# DI: Dependency Injection

### Date: 2024.01.08

---
### Dependency
- Controller가 Service를 통해서 기능해야 함 -> 의존관계가 있다.
- @Controller 어노테이션이 있으면, 스프링 컨테이너가 해당 클래스를 bean으로 관리한다.
- service, repository  등은 하나만 생성해서 공통으로 가져다 쓰면 된다(new로 새로 만들 필요 없다).
  
### Dependency injection(의존성 주입)
- Controller 코드에서 constructor로 Service 연결 부분 작성하고 **@Autowired**로 스프링이 연결 관리.
    - **Issue**: 이 때 Service가 Spring에 의해 관리되지 않는 순수한 Java class라면 에러가 발생한다.
    - **Solve**: Service와 Reposisory도 각각 어노테이션(@)으로 스프링 bean 등록.
- DI에는 필드 주입, setter 주입, 생성자 주입 3가지 방법이 있다.
- 의존관계가 실행중에 동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장한다.
- 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 컴포넌트 스캔을 사용한다.
- 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다.
    - ex. 비즈니스 로직만 있을 때

### Srping Bean을 등록하는 2가지 방법
- Component로 직접 스프링 빈 등록하기

### Component Scan
- **@Component** 애노테이션이 있으면 스프링 빈으로 자동 등록된다.
- **@Component**를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록된다.
    - **@Controller**
    - **@Service**
    - **@Repository** 

### Spring Bean by Java Code
- **@Configuration** 어노테이션으로 설정 파일에 등록

```java
package hello.hellospring; 

import hello.hellospring.repository.MemberRepository;
import hello.hellospring.repository.MemoryMemberRepository;
import hello.hellospring.service.MemberService;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SpringConfig {
    @Bean
        public MemberService memberService() {
        return new MemberService(memberRepository());
    }
    @Bean
        public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```

### Test code 작성 예시
- 테스트 코드 작성시, @AfterEach 사용하여 repository와 service 새로 할당.
- Service 입장에서 외부의 repository를 입력받는다. 

**Before DI**
```java
class MemberServiceTest {

    MemberService memberService = new MemberService();
    MemoryMemberRepository memberRepository = new MemoryMemberRepository();

    @AfterEach
    public void afterEach() {
        memberRepository.clearStore();
    }
```
  
**After DI**
```java
class MemberServiceTest {

    MemberService memberService;
    MemoryMemberRepository memberRepository;

    @BeforeEach
    public void beforeEach() {
        memberRepository = new MemoryMemberRepository( );
        memberService = new MemberService(memberRepository);
    }

    @AfterEach
    public void afterEach() {
        memberRepository.clearStore();
    }
```