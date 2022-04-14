TDD

- 애자일 개발 방식 중에 하나이다

- 테스트 주도 개발

- 코드 작성 후에 테스트를 진행한다

- 코드 설계시 원하는 단계적 목표에 대해 설정하여 진행하고자 하는 것에 대한 결정방향의 갭을 줄이고자 함

- 최초 목표에 맞춘 데스트를 구축하여 그에 맞게 코드를 설계하기 때문에 보다 적은 의견 충돌을 기대할 수 있음

  

테스트 코드를 작성하는 이유

- 코드의 안정성을 높힐 수 있다 -> 코드의 목표

- 기능 추가시에 발생하는 부작용을 줄일 수 있음

- 해당 코드가 작성된 목적을 명확하게 표현할 수 있다 -> 관련된 내용만이 들어가게 된다 테스트 코드 없이 하면 코드가 더 추가될 수 있음

  

JUnit

- Java 진영의 대표적인 Test Framework

- 단위 테스트를 위한 도구

- 단위 테스트 : 코드의 모듈이 의도된 대로 동작하는지 테스트하는 절차, 모든 함수와 메소드에 대한 각각의 테스트 케이스를 작성한다

- 어노테이션을 기바능로 테스트 지원

- assert로 테스트 케이스의 기대값에 대해 수행 결과를 확인할 수 잇음

- Junit5 버전을 사용한다

  

모듈에 대한 설명

Jupiter - TestEngine API 구현체

Platform - Test를 실행하기 위한 뼈대, TestEngine 인터페이스, 각종 IDE를 연동, 보조하는 역할을 한다

Vintage - Junit 3,4 를 구현한 TestEngine API 구현체

  

annotation

- @Test : 테스트용 메소드를 표현하는 어노테이션, 각각의 unit test마다 붙여준다

- @BeforeEach : 각각의 테스트 메소드가 시작되기 전에 실행되어야 하는 메소드

- @AfterEach : 각각의 테스트 메소드가 시작된 후에 실행되어야 하는 메소드

- @BeforeAll : 테스트 시작 전에 실행되어야 하는 메소드를 표현(static 처리 필요)

- @AfterAll : 테스트 종료 후에 실행되어야 하는 메소드를 표현(static 처리 필요)

- @DisplayName : 기본적인 테스트 메소드 이름이 아닌 이름을 지정 시에 사용한다

- @Disabled : 테스트를 실행하지 않게 설정하는 어노테이션

- @SpringBootTest : 통합 테스트 용도로 사용됨, @SprinbGootApplication을 찾아가서 하위의 모든 Bean 을 스캔하여 로드, Test용 Application Context을 만들어 Bean을 추가하고 MockBean을 찾아서 교체함

- ★@ExtendWith : Junit4에서의 @RunWith, Spring으로 확장한다는 말이다

- @WebMvcTest : web mvc와 관련된 controller와 관련된 단위 테스트 시에 사용됨, controller bean이 다 사용됨

- @Autowired about Mockbean : controller의 api를 테스트하는 용도인 MockMvc 객체를 주입받는다

- @MockBean : 테스트할 클래스에서 주입 받고 있는 의존성이 있는 객체에 대해 가짜 객체를 생성해준다

- @AutoConfigureMockMvc : spring.test.mockmvc의 설정을 로드하면서 MockMvc(Rest API를 테스트할 수 있는 클래스)의 의존성을 자동으로 주입

- @Import : 필요한 클래스들을 Configuration으로 만들어서 사용할 수 있다, Configuration Component 클래스도 의존성 설정할 수 있다

  

통합 테스트

- 여러 기능을 조합하여 전체 비즈니스 로직이 제대로 동작하는지 확인하는 것이 목적

- @SpringBootTest를 사용하여 진행한다

- 대규모 프로젝트에서 사용할 경우에는 테스트를 실행할때마다 모든 빈을 스캔하고 로드하는 작업이 반복되어 매번 무거운 작업을 수행해야 한다

  

단위 테스트

- 단위 테스트는 프로젝트에 필요한 모든 기능에 대한 테스트를 각각 진행하는 것을 의미한다

- org.springframework.boot:spring-boot-starter-test 디펜던시만으로도 의존성을 모두 가질 수 있다

  

FIRST 원칙

- Fast : 테스트 코드의 실행은 빠르게 진행되어야 한다

- Independent : 독립적인 테스트가 가능해야한다 -> 매번 모든 테스트를 돌려보는 것이 아니다

- Repeatable : 테스트는 매번 같은 결과를 만들어야 한다

- Self-Validating : 테스트는 그 자체로 실행하여 결과를 확인할 수 있어야 한다

- Timely : 단위 테스트는 비즈니스 코드가 완성되기 전에 구성하고 테스트가 가능해야한다, 코드가 완성되기 전부터 테스트가 따라와야 한다 (TDD를 사용하고 있으면 이 부분을 지켜야 한다)

  

SpringBootTest(webEnvironment = WebEnvironment.RAMDOM_PORT) : 실제 톰켓으로 테스트

SpringBootTest(webEnvironment = WebEnvironment.MOCK) : 실제 톰켓을 올리는게 아니라 다른 톰켓으로 테스트

  

MockMvc : controller 주소로 테스트해볼 수 있는 라이브러리, @AutoConfigureMockMvc가 되어있으면 메모리에 띄워준다

@Transactional : 각각의 메소드들에 대해서 롤백을 해준다

  
  

## Service 테스트

Service 단위 테스트 시에는 Repository를 들고 메모리에 띄워야하는데

그러려면 가짜 객체를 만들어주어야 한다

MockiotoExtension이 그 역할을 해준다

@ExtendedWith(MockitoExtension.class)

  

@Mock

private BookService bookService; //이렇게 해준다

근데 여기서 보통 Service에서는 Repository를 injection 받는데 테스트 시에는

Service만 메모리에 올려서 Repository에는 null이 들어가게 된다 그럴때는

@InjectMocks를 하면 해당 파일에 @Mock로 등록된 모든 애들을 주입받게 된단

그래서 @Mock로된 bookRepository가 가짜 객체로 만들어져서 들어가게 된다

## repository 테스트

@AutoConfigure TestDatabase(replace = Replace.ANY) // 가짜 DB로 테스트한다

@DataJpaTest // Repository들을 IOC에 등록해준다