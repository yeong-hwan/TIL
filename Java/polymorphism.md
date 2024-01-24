# Polymorphism

### Date: 2024.01.23

---

### Polymorphism(다형성)
- 세상을 **역할**과 **구현**으로 구분
- 예시
  - 역할: inteface
  - 구현: 구현 객체
- 클라이언트(사용자)는 구현이 변경되어도 역할을 수행하는 데 지장이 없다.
- 유연하고 변경에 용이하다.

### 장점
- 클라이언트는 대상의 역할(인터페이스)만 알아도 된다.
- 클라이언트는 대상의 내부 구조를 몰라도 된다(내부 구조가 변경되어도 영향을 받지 않는다).
- 클라이언트는 **구현 대상 자체를 변경**해도 영향을 받지 않는다.


- Java의 다형성은 Overriding으로 동작한다.

### 다형성의 본질
- 인터페이스를 구현한 객체 인스턴스를 실행 시점에 유연하게 변경할 수 있다.
- 다형성의 본질을 이해하려면 협력이라는 객체 사이의 관계에서 시작해야 한다.
- 클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있다.