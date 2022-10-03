### 비즈니스 요구사항 정리

#### 💡일반적인 웹앱 계층 구조
![3](https://user-images.githubusercontent.com/60287901/189602107-7567f3eb-0155-48ff-bc51-8ce1abf0d3e1.png)

> 컨트롤러: 웹 MVC의 컨트롤러 역할
서비스: 핵심 비즈니스 로직 구현
리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
도메인: 비즈니스 도메인 객체 ex) 회원, 주문, 쿠폰 등등 주로 DB에 저장하고 관리됨

#### 💡클래스 의존관계
* 인터페이스를 구현하여 변경 용이성 올리기

______________________

	Optional.ofNullable(store.get(id));
- null 값인 경우 에러 발생할 수 있으므로 Optional로 묶어서 return함 (Java 8부터!)

----------------

### 회원 레포지토리 테스트 케이스 작성

* 여러 함수를 Testing 한다면 @AfterEach를 이용하여 Testing마다 생긴 레포를 clear 해줘야한다.

---------
### 회원 서비스 개발
서비스는 비지니스 롤에 맞게 naming 해야함


### 회원 서비스 테스트
	Ctrl+shift+T -> create Test
    테스트 코드에서는 파일명 한글 가능함 (build될 때 실제 코드에 포함되지 않기 때문!)
    
 
```
class MemberServiceTest {
    MemberService memberService = new MemberService();
    MemoryMemberRepository memberRepository = new MemoryMemberRepository();
    
public class MemberService {

    private final MemberRepository memberRepository = new MemoryMemberRepository();
```
📍new로 객체 여러개 생성하지 말고 constructor 생성해서 재사용하도록 코드 작성하자.

> ✔️dependecy injection

```
public class MemberService {

    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
}
class MemberServiceTest {
    MemberService memberService;
    MemoryMemberRepository memberRepository;
    //repo clear를 위해 생성
    @BeforeEach
    public void beforeEach(){
        memberRepository = new MemoryMemberRepository();
        memberService = new MemberService(memberRepository);
    } 
```
