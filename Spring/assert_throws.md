# Try-Catch vs assertThrows

### Date: 2024.01.07

---

### assertThrows

* Test code 작성시, Try-Catch 보다 assertThrows를 사용하는 것이 권장된다.
* 예외 경우 터지는 Exception class를 1차로 비교.
* 필요시 해당 Exception을 변수화하여 에러 메세지를 2차로 비교한다.

**Try-Catch**

```java
    @Test
    public void dupliacteJoinTest() {
        // given
        Member member1 = new Member();
        member1.setName("duplicated name");

        Member member2 = new Member();
        member2.setName("duplicated name");

        // when
        memberService.join(member1);
        try {
            memberService.join(member2);
            fail();
        } catch (IllegalStateException e) {
            assertThat(e.getMessage()).isEqualTo("Already signed  up member");
        }

        // then
    }
```

**assertThrows**

```java
    @Test
    public void dupliacteJoinTest() {
        // given
        Member member1 = new Member();
        member1.setName("duplicated name");

        Member member2 = new Member();
        member2.setName("duplicated name");

        // when
        memberService.join(member1);

        // then
        IllegalStateException e = assertThrows(IllegalStateException.class, () -> memberService.join(member2));
        assertThat(e.getMessage()).isEqualTo("Already signed up member");
    }
```
