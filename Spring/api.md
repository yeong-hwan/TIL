# API

### Date: 2024.01.05

---

### API
<!-- * Training code repo: [repo_name](link) -->

* Software Engineering 수업의 Itrust2 Project에서 Spring을 사용할 때 애매했던 부분이다.
    * API 쓸 때 ResponseBody 태그는 왜 붙이는가?
* 이전 세대에는 html 코드(정적 컨텐츠)를 front로 보내주었지만, Spring에서는 Json 형태로 데이터를 전송.
* 이러한 방식을 API라고 한다.
* **@ResponseBody**: 객체가 Json으로 변환됨.
* ResponseBody를 사용하면 View Resolver를 사용하지 않음.

```java
@Controller
public class HelloController {
    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
            Hello hello = new Hello();
            hello.setName(name);
            return hello;
        }
        static class Hello {
            private String name;
            public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
    }
}
```

![](img/api_1.png?raw=true)