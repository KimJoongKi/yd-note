# 실전! 스프링

### gradle
-   의존관계가 연결되어있는 모든 lib를 가져온다.

``./gradlew dependencies``


### thymeleaf

- 자동으로 controller에서  리턴되는 String 파일명을 가진 html 파일을 호출한다.
- SpringBoot 설정에서 수정이 가능하다.
- resources - static 렌더링이 필요하지 않은 html 파일
- resources - templates 렌더링이 필요한 파일을 둔다.


### H2 Database

- 데이터베이스 파일 생성 방법
- jdbc:h2:~/jpashop (최소 한번)
- ~/jpashop.mv.db 파일 생성 확인
- 이후 부터는 jdbc:h2:tcp://localhost/~/jpashop 이렇게 접속

### 데이터베이스 설계

### 엔티티 클래스 개발






