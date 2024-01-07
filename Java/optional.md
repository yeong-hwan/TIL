# Optional

### Date: 2024.01.07

---
### NPE(Null Pointer Exception)
- 가장 흔한 예외 중 하나
- null 검사로 인해 코드가 복잡, 번거로워짐.
- 때문에 초기값 사용을 권장하기도 한다.

```java
List<String> names = getNames();
names.sort(); // names가 null이라면 NPE가 발생함

List<String> names = getNames();
// NPE를 방지하기 위해 null 검사를 해야함
if(names != null){
    names.sort();
}
```

### optional이란?
- optional은 변수를 감싸주는 wrapper 클래스이다.
- Optional.empty()를 통해 null 생성
- Optional.of(value)를 통해 value 생성
- optional.get()으로 value 꺼내기.

```java
Optional<String> optional = Optional.empty();

System.out.println(optional); // Optional.empty
System.out.println(optional.isPresent()); // false
```


### References
[[Java] Optional이란? Optional 개념 및 사용법](https://mangkyu.tistory.com/70)