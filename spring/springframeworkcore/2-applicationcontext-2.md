---
description: >-
  ApplicationContext의 다양한 기능들에 대해 알아보자 (ApplicationEventPublisher,
  ResourceLoader)
---

# 스프링 프레임워크 핵심기술 3 - ApplicationContext의 다양한 기능\(2\)

지난번 포스팅에 ApplicationContext의 다양한 기능 중에  Environment\(프로퍼티, 프로파일\)을 가져올 수 있는 EnvironmentCapable과 국제화\(i18n\)메세지를 관리하는 MessageSource에 대해 알아봤습니다.

이번 포스팅에서는 **`ApplicationEventPublisher`**와 **`ResourceLoader`**에 대해 알아보겠습니다.

### ApplicationContext의 다양한 기능 1 - ApplicationEventPublisher

스프링 **`ApplicationEventPublisher`**는 스프링에서 이벤트 프로그래밍에 필요한 인터페이스를 제공합니다.   
publishEvent\(\) 메소드를 통해 스프링 기반 어플리케이션에서 이벤트를 발생시킬 수 있죠. 이벤트 퍼블리셔를 사용하기 위해선 먼저 이벤트 객체가 필요합니다.

```java
public class MyEvent /*extends ApplicationEvent  
   -- Spring 4.2 버전이후 ApplicationEvnet를 상속 받을 필요 없어졌다.*/
{  
   
    private int data;
    private Object source;

    public MyEvent(Object source, int data) {
        this.source = source;
        this.data = data;
    }
    public Object getSource() {
        return source;
    }
    public int getData() {
        return data;
    }
}
```

이벤트 객체는 다음과 같이 만들어줄 수 있습니다. 기존에는 **`ApplicationEvent`**를 상속받아야 사용이 가능했지만 Spring 4.2버전 이후로는 따로 상속 받을 필요가 없습니다.

자 이제 이벤트 객체는 존재합니다. 하지만 이벤트를 빈에 따로 등록하지도 않았는데 어떻게 이벤트 퍼블리셔로 이벤트를 발생시킬 수 있을까요? 또 어떤 로직을 구현할 지는 아무것도 정해진 것이 없고, 많은 이벤트 객체중에 어떤 이벤트 객체를 사용할지도 정해지지 않았습니다.

실제로 어떤 이벤트를 발생시킬 때 어떤 객체를 활용할지, 또한 어떤 로직을 담을지 결정을 해야합니다. 그리고 그 역할을 하는 것이 **EventHandler**\(이하 핸들러\) 입니다.

```java
@Component
public class MyEventHandelr /*implements ApplicationListener<MyEvent> 
-- 역시 Spring 4.2이후로는 구현할 필요없다. 대신에 메소드에 @EvnetLisnter 추가해야한다. */{

    @EventListener
    public void myEventHandler(MyEvent event) {
        System.out.println(Thread.currentThread().toString());
        System.out.println("MyEventHandler : 이벤트 받았다. 데이터는 " + event.getData());
    } 
}
```

