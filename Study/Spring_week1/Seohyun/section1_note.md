![1](https://user-images.githubusercontent.com/60287901/189538371-3ff1df97-d6d4-40b6-86ed-c12c0d0b6787.png)
> 
🍃 예전에는 maven 이었지만 요샌 전부 gradle로 옮긴 상황
🍃 SpringBoot_snapshot(아직 만드는 중)
🍃 Group : 기업 도메인 명
🍃 Artifact : 프로젝트 결과명
🍃 Dependencies : 땡겨올 라이브러리
🍃 html 만들어주는 엔진 : thymeleaf


-------------------------

Gradle은 의존관계가 있는 라이브러리를 함께 다운로드 한다.

> 🍃 스프링 부트 라이브러리
- spring-boot-starter-web
    - spring-webmvc
    - spring-boot-starter-tomcat
- spring-boot-starter-thymeleaf:타임리프 템플릿 엔진(View)
- spring-boot-starter(공통): 스프링부트+스프링코어+로깅
	- spring-boot
    	- spring core
    - spring-boot-starter-logging
		- 실무에서는 println을 잘 안씀. 서버는 log로 관리해야함
		- slf4j & logback 조합으로 logging
 
> 🍃 테스트 라이브러리
- spring-boot-starter-test
	- junit: 테스트 프레임워크
    - mokeito : 목 라이브러리
    - assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    - spring-test: 스프링 통합 테스트 지원

-----------
[ VIEW ]

** 참고사이트
https://spring.io/
web -> index 검색하면 welcome page 나옴

https://www.thymeleaf.org/
https://spring.io/guides/gs/serving-web-content/ : 스프링 튜토리얼
https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.template-engines : 스프링부트 템플릿엔진

![2](https://user-images.githubusercontent.com/60287901/189538380-c66f1af5-1ca2-4671-80fb-61429c5ca3c3.png)

> 🍃 터미널에서 gradle 빌드하고 돌리는 경우

	./gradlew.bat build
	cd build/libs
	java -jar xxxx.jar
	./gradlew.bat clean -> 기존 빌드 파일 삭제
