# DI: Dependency Injection

### Date: 2024.01.08
- 2024.01.14: Addition explanation details about DI

---
## Dependency
- 의존성(의존관계)이 있다 : 한 객체가 다른 객체를 사용한다.
    -> Controller가 Service를 통해서 기능해야 함.
```java
public class Controller {
    private AlphaService alphaService

    public Controller() {
        this.alphaService = new AlphaService();
    }
}
```
위의 예시는 다음과 같은 문제점을 가진다.
1. Controller와 Alphaservice가 강하게 결합되어 있다.
    - 만약 Controller가 AlphaService가 아닌 다른 클래스를 연동하고자 한다면, Controller의 생성자 변경이 필요하다.
    -> 유연성이 떨어진다.
    - 상속은 제약이 많고 확장성이 떨어지므로 피하는 것이 좋다.

2. **객체**들 간의 관계가 아니라 **클래스** 간의 관계가 맺어졌다.
    - 올바는 OOP 설계라면 객체들 간의 관계가 맺어져야 한다.
    - 객체들 간의 관계가 맺어졌다면, 다른 객체의 구체 클래스(AlphaService, BetaService 등)을 알지 못 하더라도, 인터페이스(Service)의 타입으로 사용할 수 있다.


### 의존성 주입(Dependency Injection)을 통한 문제 해결
- 위와 같은 문제를 해결하기 위해서 다형성이 필요하다.
- Serivce라는 Interface를 통해 해결한다(Controller에서 구체 클래스에 의존하지 않게 된다).
```java
public interface Service {

}

public class AlphaService implements Service {

}
```
- 이제 Controller와 AlphaService가 강하게 결합되어 있는 부분을 Injection으로 변경해준다.

```java
public class Controller {
    private Service service;

    public Controller(Service service) {
        this.servcie = service;
    }
}
```

- Spring이라는 DI Container가 필요한 이유.
- 어플리케이션 실행 시점에 필요한 객체(Bean)을 생성하고, 의존성이 있는 두 객체를 연결하기 위해 한 객체를 다른 객체로 주입시킨다.


```java
public class BeanFactory {

    public void controller() {
        // Bean의 생성
        Product AlpahService = new Service();
    
        // 의존성 주입
        Controller controller = new Controller(AlphaService);
    }
    
}
```

## Code에서의 적용

- @Controller 어노테이션이 있으면, 스프링 컨테이너가 해당 클래스를 bean으로 관리한다.
- service, repository  등은 하나만 생성해서 공통으로 가져다 쓰면 된다(new로 새로 만들 필요 없다).
  
### Dependency injection(의존성 주입)
- 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴
- 인터페이스를 사이에 둬서, 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입
    -> 유연성 확보하고 결합도를 낮춘다.


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

---
### References
[[Spring] 의존성 주입(Dependency Injection, DI)이란?](https://mangkyu.tistory.com/150#recentEntries)