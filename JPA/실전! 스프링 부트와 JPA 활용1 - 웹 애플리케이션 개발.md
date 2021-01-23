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

~~~java
@JoinTable(name = "category_item",
        joinColumns = @JoinColumn(name = "category_id"),
            inverseJoinColumns = @JoinColumn(name = "item_id"))
// 관계형 테이블? 추가적인 컬럼을 추가할 수 없기 때문에 실무에서는 사용되지 않는다.
~~~ 

> JPA 스펙상 엔티티나 임베디드 타입( @Embeddable )은 자바 기본 생성자(default constructor)를 
> public 또는 protected 로 설정해야 한다. 
> public 으로 두는 것 보다는 protected 로 설정하는 것이 그나마 더 안전하다.
> JPA가 이런 제약을 두는 이유는 
> JPA 구현 라이브러리가 객체를 생성할 때 리플랙션 같은 기술을 사용할 수 있도록 지원해야 하기 때문이다.


* * *

#### 엔티티에는 가급적 Setter를 사용하지 말자
- Setter가 모두 열려있으면 변경 포인트가 너무 많아서, 유지보수가 어렵다.

#### 모든 연관관계는 지연로딩으로 설정!
- 즉시로딩( EAGER )은 예측이 어렵고, 어떤 SQL이 실행될지 추적하기 어렵다. 
  특히 JPQL을 실행할 때 N+1 문제가 자주 발생한다.
- 실무에서 모든 연관관계는 지연로딩( LAZY )으로 설정해야 한다.
- 연관된 엔티티를 함께 DB에서 조회해야 하면, fetch join 또는 엔티티 그래프 기능을 사용한다.
- @XToOne(OneToOne, ManyToOne) 관계는 기본이 즉시로딩이므로 직접 지연로딩으로 설정해야 한
  다
  


* * *

### CASCADE
