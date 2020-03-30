## ApplicationEventPublisher

> 이벤트 프로그래밍에 필요한 인터페이스 제공. 옵저버 패턴 구현체

- ApplicationContext extends ApplicationEventPublisher

  - publishEvent(ApplicationEvent event)
  
- 이벤트 만들기

  - ApplicationEvent 클래스 상속
  
  - 스프링 4.2 부터는 상속받지 않아도 이벤트로 사용 할 수 있음
  
  - **빈으로 등록될 필요 X** (비침투성: 스프링 프레임워크의 코드가 노출되지 않도록, POJO)
  
  ```java
  //ApplicationEvent 클래스 상속 필수 X
  //상속 받지 않고 source를 얻고 싶다면 private Object source를 필드로
  public class MyEvent extends ApplicationEvent {
  
    //전달하고자 하는 데이터
    private int data;
    //private Object source;
    
    public MyEvent(Object source, int data) {
      super(source);
      this.data = data;
    }
    
    public int getData() {
      return data;
    }
  }
  ```

- 이벤트 발생시키는 방법

  - ApplicationEventPublisher.publishEvent()
  
  ```java
  @Component
  public class AppRunner implements ApplicationRunner {
  
    //ApplicationContext 타입도 가능
    @Autowired
    ApplicationEventPublisher publishEvent;
    
    @Override
    public void run(ApplicationArguments args) throws Exception {
      publishEvent.publishEvent(new MyEvent(this, 100));
    }
  }
  ```
  
- 이벤트 처리하는 방법

  - ApplicationListener<이벤트> 인터페이스를 구현한 클래스 만들어 **빈으로 등록**
  
  - 스프링 4.2 부터는 인터페이스 구현 없이 **@EventListener**를 빈의 메소드에 사용 가능
  
  - **이벤트에 대한 핸들러가 여러개**일 때 기본적으로는 순차적으로 실행(synchronized)
  
  - 순서를 정하고 싶다면 *@Order*과 함께 사용
  
  - 비동기적으로 실행하고 십다면 *@Async*와 함께 사용(순서 보장 X)
  
    - 다수의 쓰레드 사용위해 *@EnableAsync*도 (메인 메소드 클래스에) 함께 필요
  
  ```java
  //인터페이스 구현
  @Component
  public class MyEventHandler implements ApplicationListener<MyEvent> {
  
    @Override
    public void onApplicationEvent(MyEvent event) {
      System.out.println("Event Occured! Data = " + event.getData());
    }
  }
  ```
  
    ```java
  //인터페이스 구현 없이
  @Component
  public class MyEventHandler {
  
    //인터페이스를 구현하지 않으므로 메소드명 또한 자유
    @EventListener
    //Order.HIGHEST_PRECEDENCE + n 형식으로 우선순위 지정
    @Order(Order.HIGHTEST_PRECEDENCE)
    public void myMethod(MyEvent event) {
      System.out.println("Event Occured! Data = " + event.getData());
    }
  }
  ```
  
- 스프링이 제공하는 기본 이벤트

  - ContextRefreshedEvent: ApplicationContext를 초기화하거나 리프레시 했을 때 발생
  
  - ContextStartedEvent: ApplicationContext를 start()하여 라이프사이클 빈들이 시작 신호를 받은 시점에 발생
  
  - ContextStoppedEvent: ApplicationContext를 stop()하여 라이프사이클 빈들이 정지 신호를 받은 시점에 발생
  
  - ContextClosedEvent: ApplicationContext를 close()하여 싱글톤 빈들이 소멸되는 시점에 발생
  
  - RequestHandledEvent: HTTP 요청을 처리했을 때 발생
