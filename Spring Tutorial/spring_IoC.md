# Spring IoC(Inversion of Control)

- 일반적인 의존성 제어권: **"내가 사용할 의존성은 내가 만든다."**

```java
class OwnerController {
  private OwnerRepository repo = new OwnerRepository();
  
  //repo 사용
}
```

- IoC(제어권 역전): **"내가 사용할 의존성을 누군가 알아서 주겠지."**

```java
class OwnerController {
  private OwnerRepository repo;
  
  //OwnerRepository 없이는 OwnerController를 생성할 수 없음(NullPointerException 방지)
  public OwnerController(OwnerRepository repo) {
    this.repo = repo;
  }
  
  //repo 사용
}
```

```java
class OwnerControllerTest {
  //의존성 주입
  @Test
  public void create() {
    OwnerRepository repo = new OwnerRepository();
    OwnerController controller = new OnwerController(repo);
    controller.doSomething();
  }
}
```

- Spring Bean: Spring IoC 컨테이너에 의해 인스턴스화, (의존성) 관리, 생성되는 객체(*@MockBean*)

