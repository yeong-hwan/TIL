# Spring Data JPA

### Date: 2024.01.16

---

### Spring Data JPA
- 리포지토리에 구현 클래스 없이 인터페이스만으로 개발을 완료할 수 있다.
- JPA에서 반복 개발해온 기본 **CRUD, 단순 조회**도 스프링 데이터 JPA가 모두 제공한다.
  - 인터페이스를 통한 기본적인 CRUD
  - findByName() , findByEmail() 처럼 메서드 이름 만으로 조회 기능 제공
  - 페이징 기능 자동 제공
### Spring Data JPA Repository
```java
public interface SpringDataJpaMemberRepository extends JpaRepository<Member,Long>, MemberRepository {
    Optional<Member> findByName(String name);
}
```

### Spring Config
- 스프링 데이터 JPA가 SpringDataJpaMemberRepository 를 스프링 빈으로 자동 등록해준다.
```java
@Configuration
public class SpringConfig {

    private final MemberRepository memberRepository;

    public SpringConfig(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository);
    }
}
```

### Note
- 실무에서는 **JPA**와 **스프링 데이터 JPA**를 기본으로 사용하고, 복잡한 동적 쿼리는 **Querydsl**이라는 라이브러리를 사용한다.
  - Querydsl을 사용하면 쿼리도 자바 코드로 안전하게 작성할 수 있고, 동적 쿼리도 편리하게 작성할 수 있다.
  - 이 조합으로 해결하기 어려운 쿼리는 JPA가 제공하는 **네이티브 쿼리**를 사용하거나, **Spring JdbcTemplate**를 사용하면 된다.