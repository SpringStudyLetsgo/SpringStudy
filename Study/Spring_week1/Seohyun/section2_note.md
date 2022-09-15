스프링 웹 개발 기초

- 정적 컨텐츠 : 서버에서 뭐 하는거 없이 파일을 그대로 웹 브라우저에 내려주는 것
- MVC와 템플릿 엔진 : JSP, PHP 등 서버에서 프로그래밍 한 후 HTMl을 동적으로 변경한 뒤에 브라우저에 내려주는 것
- API : JSON으로 데이터를 전달하는 방식. Vue.js 사용시 API방식 많이 사용.
서버끼리 통신할 때도 API 사용 (데이터가 흐르는 것 = API 방식)



-----------------------
### 정적 컨텐츠
> 1. hello-static.html을 치면 내장 톰켓 서버가 요청을 받아서 Spring에 넘김
2. 컨트롤러(우선순위 1)가 hello-static 과 매핑되는 컨트롤러를 찾음
3. 없으면 resources 파일 하위에 hello-static.html 있는지 찾고 실행시킴

### MVC와 템플릿 엔진
* 과거에는 컨트롤러와 뷰가 분리되어 있지 않았음
* 모델에 파라미터를 넘기고 해당 파라미터 값을 불러와서 브라우저에 띄움

> hello-mvc 요청 -> 내장 톰캣 서버가 받음 -> 스프링 컨테이너에 도착 -> helloController 안에 매핑된 컨트롤러가 있음을 확인함 -> hello-template을 리턴하고 해당 메소드 호출함 -> viewResolver는 view를 찾고 템플릿 엔진을 연결해줌 -> template 하위에 있는 hello-template.html을 찾고 랜더링을 거쳐 변환을 한 html을 웹브라우저에 넘김


### API방식

@ResponseBody : http에서 responsebody부에 응답 내용을 넣겠다는 어노테이션
뷰 따로 없이 return 문자열이 그대로 내려감
```
http://localhost:8080/hello-string?name=spring!!
```
* Get 방식의 url 작성
* xml은 json보다 무거워서 json을 많이 사용하는 추세


```
  @GetMapping("hello-api")
  @ResponseBody
  public Hello helloApi(@RequestParam("name") String name ){
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }
    static class Hello{
        private String name;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
```
> hello-api 요청 -> 내장 톰캣 서버가 받음 -> 스프링 컨테이너에 도착 -> helloController 안에 @ResponseBody가 있다면 -> http 응답에 body를 넘겨줌. 이때 객체가 오면 Json 방식으로 데이터를 만들어서 http 응답에 반응을 함 -> HttpMessageConverter(JsonConverter:객체인 경우/// StringConverter:문자열인 경우) -> (name:string) 반환


