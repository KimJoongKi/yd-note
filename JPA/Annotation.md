# Annotation

## @Builder

### build() 메소드를 자동으로 추가해주는 Annotation
- #### 예제
```java
// 사용 전
@Getter @Setter
public class User {
    
    private String name;
    private int age;
    
    public static UserBuilder builder() {
        return new UserBuilder();
    }
}

public class UserBuilder {
    private String name;
    private int age;
    
    public User build() {
        User user = new User();
        user.setName(this.name);
        user.setAge(this.age);
        return user;
    }

    public UserBuilder name(String name) {
        this.name = name;
        return this;
    }
}

public class UserBuilderTest {
    @Test
    public void builderTest() {
        User user = User.builder()
                .name("홍길동")
                .age(19)
                .build();
        System.out.println(user);
    }
} 

// 사용 후
@Getter @Setter @Builder
public class User {
    private String name;
    private int age;
}

public class UserBuilderTest {
    @Test
    public void builderTest() {
        User user = User.builder()
                .name("홍길동")
                .age(19)
                .build();
    }
}
```

### @Builder 사용시 default값 설정

#### 예제

```java
@Builder @Getter @Setter
public class User {
    private String name;
    @Builder.Default private int age = 19;
}

public class UserBuilderTest {
    @Test
    public void builderTest() {
        User user = User.builder()
                .name("홍길동")
                .build();
    }
}
```
> 1.16.16 버전 이상부터 가능<br>
> Default를 추가하지 않으면 0, false, null로 설정된다.

> 출처 : https://tomining.tistory.com/180