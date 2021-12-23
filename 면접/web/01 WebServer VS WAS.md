# WebServer VS WAS.md
## 📖 `웹 서버` 와 `WAS`

### 📄 웹 서버

`HTTP`를 기반으로 동작하는 웹 애플리케이션을 위한 정적 서버이다.
주로, **정적 리소스를 제공**하고 이 외에도 기타 부가 기능을 제공한다.

**정적 리소스(파일)이란? 🤔**

- HTML
- CSS
- JS
- 이미지
- 영상 등등..

우리가 알만한 대표적인 웹 서버로는 `Nginx` 와 `Apache`가 있다.

### 📄 웹 애플리케이션 서버(WAS)

`HTTP`를 기반으로 동작하는 웹 애플리케이션을 위한 **동적 서버**이다.
기본적인 **웹 서버 기능(정적 리소스 제공)은 물론,  
프로그램 코드를 실행해서 애플리케이션 로직을 수행한 동적 리소스를 제공해준다.**

**동적 리소스란? 🤔**

- 동적 HTML
- HTTP API(JSON)

**WAS는 애플리케이션 코드를 실행하는데 더 특화되어 있다.**

## 📖 웹 시스템 구성 요소

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/716ed817-a0cd-4a77-831c-0575cc5a13b8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/716ed817-a0cd-4a77-831c-0575cc5a13b8/Untitled.png)

`WAS`는 정적 리소스, 애플리케이션 로직 모두 제공이 가능하기에
`WAS + DB` 정도만 있어도 가장 기본적인 웹 시스템 환경을 구성할 수 있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f7c6b6a-3ab5-4e7a-87ec-b50ce90ca625/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f7c6b6a-3ab5-4e7a-87ec-b50ce90ca625/Untitled.png)

그러나, 이렇게 `단일 WAS` 로만 시스템을 구축을 하게 된다면
**WAS에 장애가 발생했을시(죽을시) 가용 서버 자체가 없기에 오류 화면도 노출 불가능하며
WAS가 너무 많은 역할을 담당하게 되기에 오히려 서버 과부하가 발생할 수 있다.**

이러한 문제를 해결하기 위해서 개발자는 **관심사 분리**
즉, `웹 애플리케이션 서버` 앞에 `일반 웹 서버(프록시 서버)`를 놓는 방식을 권장하고 있다.

### 📄 프록시 서버(관심사의 분리)

`WAS`만을  사용했을 때 발생하는 문제점을 해결하기 위해
`WAS` 앞에 `일반 웹 서버`를 놓는 `프록시 서버` 방식을 이용한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c590ab68-7cf5-44ed-b371-ebbd1de7ac5b/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c590ab68-7cf5-44ed-b371-ebbd1de7ac5b/Untitled.png)

**정적 리소스에 대한 요청**은 **프록시 서버(웹 서버)가 처리**를 하고
**애플리케이션 로직과 같은 동적인 처리**가 필요하면, **WAS에 요청을 위임**한다.
결과적으로 **WAS는 중요한 애플리케이션 로직 처리만 전담하게 된다.**

이 과정에서  `정적 리소스`는 값이 변하지 않으므로 **캐시 사용할 수 있으며(CDN) 적극 권장하며**   
`로드밸런싱`, `HTTP2 프르토콜로 변환` , `CERT 보안`, `오류화면 노출` 기능들도 활용할 수 있다.
(`gzip 압축`, `지연 로딩`등 정적 리소스에 대한 **웹 성능 향상 작업도 할 수 있다.**)
