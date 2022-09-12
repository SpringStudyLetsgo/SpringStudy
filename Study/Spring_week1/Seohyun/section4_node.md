### 스프링 빈과 의존 관계

#### 스프링 빈을 등록하고, 의존관계 설정하기

- 본 예제에서 repository는 DB같은 느낌
- 컨트롤러와 뷰탬플릿이 있어야 화면 생김
- 멤버 컨트롤러는 멤버 서비스를 통해 가입 및 조회가 가능 ( "멤버 컨트롤러가 멤버 서비스에 의존한다" 라고 표현함)

----------------
- 서비스를 매번 new로 컨테이너에서 생성하기 보다는 컨테이너에 서비스를 등록해서 재사용을 하는 것 이 더 좋음 ! 
- 어노테이션을 달지 않으면 **순수한 자바 코드** 이므로 컨테이너에 등록하기 위해선 어노테이션 필수 !!

> 스프링 빈을 등록하는 2가지 방법
🟣 컴포넌트 스캔과 자동 의존관계 설정
🟣 자바 코드로 직접 스프링 빈 등록하기

- 컴포넌트 스캔과 자동 의존관계 설정

    - **어노테이션**으로 작성하는 것
    - 생성자에 @Autowired 를 사용하면 객체 생성 시점에 스프링 컨테이너에서 스프링 빈을 찾아서 주입한다. 또한, 생성자가 1개만 있으면 '@Autowired' 생략 가능!
    - 스프링은 스프링 컨테이너에 스프링 빈을 등록할 때 기본으로 싱글톤으로 등록함.(유일하게 하나만 등록해서 공유함)
    - 같은 스프링 빈이면 모두 같은 인스턴스!
    - 설정으로 싱글톤이 아니게 설정할 수 있지만 특별한 경우가 아니면 대부분 싱글톤으로 진행함
    
- 자바 코드로 직접 스프링 빈 등록하기
	- 어노테이션 사용 안함!
    - 직접 자바 코드를 스프링에 등록하는 것
    
1. 필드 주입 _ 잘 사용하지 않음!
```
    @Autowired private MemberService memberService;
```
2. 생성자 주입
```
    private final MemberService memberService;
    @Autowired

    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
```
3. Setter 주입
```
    private MemberService memberService;
    @Autowired

    public void setMemberService(MemberService memberService) {
        this.memberService = memberService;
    }
```
📍의존 관계가 런타임 중간에 동적으로 변하는 경우는 없으므로 **생성자 방식**을 주로 사용한다.

> 주의: **@Autowired 를 통한 DI**는 helloController , memberService 등과 같이 **스프링이 관리하는 객체**에서만 동작한다. 
스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 **동작하지 않는다.**
