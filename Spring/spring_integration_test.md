# Spring Integration Test

### Date: 2024.01.10

---

### Integration Test
<!-- * Training code repo: [repo_name](link) -->

- 통합 테스트는 단위 테스트와 달리 개발자가 변경할 수 없는 부분(ex. 외부 라이브러리)까지 묶어 검증할 때 사용한다.
- DB에 접근하거나 전체 코드와 다양한 환경이 제대로 작동하는지 확인하는데 필요한 모든 작업을 수행할 수 있다.

### Annotation

- **@SpringBootTest**: 통합 테스트를 제공하는 기본적인 스프링 부트 테스트 어노테이션
  - 실제 구동되는 애플리케이션과 똑같이 ApplicationContext를 로드하여 테스트.

- **@Transactinal**
  - 테스트 메서드에 @Transactional을 사용하면 트랜잭션으로 감싸지며, 메서드가 종료될 때 자동으로 롤백된다. 
- **@Autowired**
  - 알아서 의존 객체(Bean)을 찾아서 주입한다

- Test Case는 필요한 것만 Injection해서 쓰고 끝나기 때문에, 필드 기반 @Autowired 받는 것도 좋다.

### Unit Test(DI)
```java
class MemberServiceTest {

    MemberService memberService;
    MemoryMemberRepository memberRepository;

    @BeforeEach
    public void beforeEach() {
        memberRepository = new MemoryMemberRepository( );
        memberService = new MemberService(memberRepository);
    }
}
```

### Integration Test(@Autowired)
```java
@SpringBootTest
@Transactional
class MemberServiceIntegrationTest {

    @Autowired MemberService memberService;
    @Autowired MemberRepository memberRepositoy;
}
```