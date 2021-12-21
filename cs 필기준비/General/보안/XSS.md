# XSS(Cross Site Script)
> 사이트 간 스크립팅       
                
 악의적인 사용자가 공격하려는 사이트에 스크립트를 넣는 기법을 말한다.            
 특정 사이트로 리다이렉트하거나 사용자의 쿠키를 탈취하여 세션 하이재킹을 한다.           
      
**대표적인 공격 방식** 
* Stored XSS   
* Reflected XSS  
* DOM based XSS   

# StoredXSS     
   
공격자의 데이터가 서버에 저장된 후,   
지속적으로 서비스를 제공하는 정상 페이지에서 다른 사용자에게 스크립트 노출되는 기법           
       
**방식**          
1. 악의적인 스크립트를 데이터베이스에 저장하도록 한다.               
2. 해당 데이터를 사용하는 순간 해당 스크립트를 실행하게 한다.              
3. 주로, 데이터베이스내의 민감한 정보들을 탈취하기 위한 작업등으로 사용된다.          
  
# Reflected XSS     
웹 어플리케이션의 지정된 파라미터를 사용할 때 발생하는 취약점을 이용한 공격 기법          
URL 쿼리파라미터에 스크립트를 포함시켜 응답 페이지에 해당 스크립트를 실행하도록 하는 기법이다.    
      
* 공격용 스크립트가 대상 웹사이트에 있지 않고 다른 매체(타 사이트, 메일)에 포함될 수 있다.   
* Stored XSS와는 다르게 데이터베이스에 스크립트가 저장되지 않고 **응답 페이지에 바로 클라이언트에 전달**되는 차이점이 있다.      
  
**방식**    
1. 해커가 악의적인 스크립트를 URL에 담아 공유     
2. 응답 페이지에서 해당 스크립트가 실행되어 악의적인 컴포넌트를 생성한다.(피싱)    
3. 사용자가 피싱되어 해당 컴포넌트의 URL을 클릭하면 추가 스크립트를 발생시킬 수 있다.       

# XSS 공격 방지   
## 1. XSS 취약점이 있는 innerHTML 사용을 자제한다.     
* 다행히도 HTML5에서는 innerHTML을 통해 주입한 스크립트는 실해되지 않는다.     
  * e.g. `<script>alert('hello');</script>`            
* 하지만 여전히 스크립트를 실행할 방법이 있긴하다.        
  * e.g. onerror 이벤트 속성을 통한 스크립트 주입      
  * `<img src="" onerror=alert('xss attack')>`         
* 그러므로 꼭 필요한 경우가 아니라면 innerHTML을 통해 검증되지 않은 데이터를 넣지 말자      
* **textContent, innerText를 사용하면 스크립트가 주입되지 않는다.**    
   
### 실 사용 서비스에서는 어떻게 처리하고 있을까?   
**N사**     
* 직접 블로그 HTML 에디터에 아래 스크립트를 삽입해보니   
  * `<img src=x onerror="alert('xss attack')">`
* 입력한 태그가 아래와 같이 치횐되었다! (서버에서 치환 처리)   
  * `<!-- Not Allowed Attribute Filtered (src="x")--> `
  * `<img class="__se_object" s_type="attachment" s_subtype="image" jsonvalue="%7B%7D">` 
  *  서버단에서 처리하는 것으로 확인할 수 있었다.      

### Vue.js와 같은 프레임워클 사용시 위와 같은 문제가 발생하지 않는가?   
* v-html 디렉티브 사용시 보안 취약점이 발생할 수 있다.      
  * 사용자 입력을 innerHTML와 동일한 방식으로 처리한다.       
  * 웹사이트에서 임의의 HTML 을 동적으로 렌더링하려면(XSS 취약점)   
  ( https://en.wikipedia.org/wiki/Cross-site_scripting )으로 쉽게 이어질 수 있으므로 매우 위험한 가능성이 있습니다.       
  신뢰할 수 있는 콘텐츠에서만 HTML 보안을 사용하고 사용자가 제공하는 콘텐츠에서는 **절대** 사용하면 안됩니다.       

## 2. 쿠키에 HttpOnly 옵션을 활성화한다.    
* HttpOnly 옵션을 활성화 하지 않으면 스크립트를 통해 쿠키에 접근할 수 있어 Session Hijacking 취약점 발생      
  * e.g. `https://hacker.site?name=<script>alert(document.cookie);</script>`      
* 반대로 말하면, HttpOnly를 활성화 시키면 악의적인 클라이언트가 쿠키에 저장된 정보(세ID, 토큰)에 접근하는 것을 차단한다.   
* 단, 위와 같은 경우는 쿠키에만 해당하므로 LocalStorage에 세션ID와 같은 민감한 정보를 저장하지 않는 노력도 해야한다.   
* 참고 : https://woowacourse.github.io/javable/2020-08-31/where_to_store_token    

## 3. XSS 특수문자를 치환한다.     
|from|`&`|`<`|`>`|`*`|`'`|`/`|   
|----|---|---|---|---|---|---|   
|to|`&amp;`|`&lt;`|`&gt;`|`&quot;`|`&#x27;`|`&#x2F;`|    
   
* Spring에서는 직접 구현하지 않아도 오픈소스 라이브러리를 사용하면 된다.    
  * Lucy XSS Servlet Filter: https://github.com/naver/lucy-xss-servlet-filter
    * `@RequestBody`로 전달되는 JSON 요청에 대해서는 처리해주지 않는다.  
    * 처리법을 다루기에는 내용이 길어지므로 jojoldu 님의 블로그 참조 | https://jojoldu.tistory.com/470


