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
~~~java 
- @Embeddable : 다른 엔티티의 일부로 저장될 수 있음을 설정하는 어노테이션
- @Embedded : 위 어노테이션이 있으면 적지 않아도 되지만 구분이 쉽게 상대 파리미터 위에도 명시  
- @GeneratedValue : 키값의 자동 생성을 명시하는데 사용
- 현재 파일(테이블) 기준으로 지정된 파일(테이블)과의 관계 명시
- @OneToOne , @OneToMany , @ManyToOne , @ManyToMany
    - mappedBy = "변수명"   
- @JoinColumn(name = "대상 테이블 컬럼명")    
- @Enumerated ENUM 타입 지정
    - ORDINAL : 순서 (중간에 다른 값이 들어가면 번호가 밀리는 문제가 발생할 수 있으니 절대 사용하면 X)
    - STRING : 이름
- @DiscriminatorColumn(name = "dtype") : 부모클래스를 상속받은 하위클래스들의 구분할 컬럼을 생성
- @DiscriminatorValue("A") : 부모클래스 구분 컬럼에 입력될 값을 지정
- @Inheritance(strategy = InheritanceType.SINGLE_TABLE) :
    - [JOINED, SINGLE_TABLE , TABLE_PER_CLASS]
~~~