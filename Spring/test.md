# Test

### Date: 2024.01.06

---

### Test
<!-- * Training code repo: [repo_name](link) -->

- main 메소드의 반복 실행 등 번거로움을 줄여줌(Test 관련 코드만 실행).
- 여러 테스트를 동시에 실행 및 관리할 수 있다는 이점.
- JUnit 프레임워크를 이용한다.  
- 디버깅 포인트에 대한 인지와 관리의 중요성을 배웠다.
- [테스트 코드를 왜 그리고 어떻게 작성해야 할까?](https://tech.inflab.com/20230404-test-code/)

### Caution
- 모든 테스트는 순서에 상관없이(순서에 의존하지 않게) 설계해야 한다.
- 이를 위해 **@AfterEach** 등으로 repository를 clear한다.

```java
package springintro.springintro.repository;

import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;
import springintro.springintro.domain.Member;

import java.util.List;

import static org.assertj. core.api.Assertions.*;

class MemoryMemberRepositoryTest {
    MemoryMemberRepository repository = new MemoryMemberRepository();

    @AfterEach
    public void afterEach() {
        repository.clearStore();
    }

    @Test
    public void save() {
        Member member = new Member();
        member.setName("spring test");

        repository.save(member);

        Member result = repository.findById(member.getId()).get();

        assertThat(member).isEqualTo(result);
    }

    @Test
    public void findByName() {
        Member member1 = new Member();
        member1.setName("name test 1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("name test 2");
        repository.save(member2);

        Member result = repository.findByName("name test 1").get();

        assertThat(member1).isEqualTo(result);
    }
    @Test
    public void findAll() {
        Member member1 = new Member();
        member1.setName("name test 1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("name test 2");
        repository.save(member2);

        List<Member> result = repository.findAll();

        assertThat(result.size()).isEqualTo(2);
    }
}

```

<!-- ![](img/api_1.png?raw=true) -->