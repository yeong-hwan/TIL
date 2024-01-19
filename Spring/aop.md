# AOP

### Date: 2024.01.18

---

### AOP(Aspect Oriented Programming)
공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern) 분리

**AOP가 필요한 상황?**
- 모든 메소드의 호출 시간을 측정하고 싶다면?
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)
- 회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?  

![](img/aop_1.png?raw=true)
- 시간 측정 로직을 각 Component마다 집어넣었는데, 측정 단위를 수정해야 한다면?
  ex) s -> ms
  
**Problems**
- 회원가입, 회원 조회에 시간을 측정하는 기능은 **핵심 관심 사항이 아니다.**
- 시간을 측정하는 로직은 **공통 관심 사항**이다.
- 시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 **유지보수가 어렵다.**
- 시간을 측정하는 로직을 **별도의 공통 로직으로 만들기 매우 어렵다.**
- 시간을 측정하는 로직을 변경할 때 **모든 로직을 찾아가면서 변경해야 한다.**

**Solve**
![](img/aop_2.png?raw=true)
- 회원가입, 회원 조회등 핵심 관심사항과 시간을 측정하는 공통 관심 사항을 분리한다.
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들었다.
- 핵심 관심 사항을 깔끔하게 유지할 수 있다.
- 변경이 필요하면 이 로직만 변경하면 된다.
- 원하는 적용 대상을 선택할 수 있다.

### AOP Code

```java
@Aspect
@Component
public class TimeTraceAop {

    @Around("execution(* hello.hellospring..*(..))")
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        System.out.println("START: " + joinPoint.toString());

        try {
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("END: " + joinPoint.toString() + " " + timeMs +
                    "ms");
        }
    }
}
```
- **@Aspect** 어노테이션으로 등록
- Component Scan(**@Component**)으로 등록할 수도 있지만 Spring Config에 스프링 Bean 등록하는 것이 더 적합하다.
- **@Around** 어노테이션으로 Aspect(공통 관심 사항) 로직 적용할 경로 지정

![](img/aop_3.png?raw=true)