# SOLID 원칙

### Date: 2024.01.24

---

### Single responsibility principle
- SRP 단일 책임 원칙
  - 한 클래스는 하나의 책임만 가져야 한다.
  - 하나의 책임이라는 것은 모호하다.
  - 클 수 있고, 작을 수 있다.
  - 문맥과 상황에 따라 다르다.
  - 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것
  - 예) UI 변경, 객체의 생성과 사용을 분리

### OCP: 개방-폐쇄 원칙
- Open/closed principle

```java
public class MemberService {
  // private MemberRepositoy memberRepository = new MemoryMemberRepository();
  private MemberRepositoy memberRepository = new JdbcMemberRepository();
}
```
- 문제점
  - 분명 다형성을 사용했지만 OCP 원칙을 지킬 수 없다.
  - 이 문제를 어떻게 해결해야 하나?
  - 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요하다
  -> 이를 스프링 컨테이너가 해준다.