# JPA

### Date: 2024.01.15

---

### JPA(Java Persistance API)
- JDBC Template(Spring)은 JDBC의 반복적인 코드 등을 간략화함.
  but, 여전히 SQL은 개발자가 작성해야 한다.
- JPA는 SQL Query를 자동처리해준다.
- **SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.**

- JPA는 하나의 인터페이스.
  (구현체로 Hibernate, Eclipse Link 등 구현 벤더가 있다.)

### ORM
- Object랑 Relational DB를 Mapping한다.

### Setting
- Spring Boot에 JPA 설정 추가

resources/application.properties
```properties
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none
```

- show-sql : JPA가 생성하는 SQL을 출력한다.
- ddl-auto : JPA는 테이블을 자동으로 생성하는 기능을 제공하는데 none을 사용하면 해당 기능을 끈다.
  - create 를 사용하면 엔티티 정보를 바탕으로 테이블도 직접 생성해준다.

### JPA Entity Mapping
```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

// Entity 지정
@Entity
public class Member {
    // Id 생성
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    // 만약 DB column 이름이 username일 경우
    @Column(name = "username")
    private String name;

    public Long getId() {
        return id;
    }
}
```

### JPA 회원 repository
- jpql이라는 쿼리로 작성.
- findByName, findAll 등 id(PK)기반이 아닌 것들은 jpql 쿼리로 찾아야한다.
```java
import javax.persistence.EntityManager;
import java.util.List;
import java.util.Optional;

public class JpaMemberRepository implements MemberRepository {
    
    private final EntityManager em;
    
    public JpaMemberRepository(EntityManager em) {
        this.em = em;
    }

    public Member save(Member member) {
      em.persist(member);
      return member;
    }

    public Optional<Member> findById(Long id) {
        Member member = em.find(Member.class, id);
        return Optional.ofNullable(member);
    }

    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class)
        .getResultList();
    }
    public Optional<Member> findByName(String name) {
        List<Member> result = em.createQuery("select m from Member m where
        m.name = :name", Member.class)
        .setParameter("name", name)
        .getResultList();
        return result.stream().findAny();
    }
}
```

### Transactional
서비스 계층에 **@Transactional** 추가
**jpa는 모든 데이터 변경이 Transaction 안에서 실행되어야 한다.**
- 스프링은 해당 클래스의 메서드를 실행할 때 트랜잭션을 시작하고, 메서드가 정상 종료되면 트랜잭션을 커밋한다.
- 만약 런타임 예외가 발생하면 롤백한다
```java
import org.springframework.transaction.annotation.Transactional

@Transactional
public class MemberService {}
```