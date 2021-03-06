# HTTP의 특징과 HTTP 메소드에 대해
<br>

>### 출처
> 1. 유튜브 <네트워크 기초 강의> 
> https://www.youtube.com/watch?v=TwsQX1AnWJU&list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi&index=28  
> 2. 우에노 센 저, <그림으로 배우는 Http Network Basic>

<br>

# 7계층 프로토콜 ‘HTTP’란?

- 수많은 종류의 OSI 7계층 프로토콜 중, 
‘웹’ 통신 서비스를 할 때 가장 대표적으로 쓰는 프로토콜은 ‘HTTP’  
<br>

## 1. 웹을 만드는 기술

```
HTTP(HTTPS → SSL/TSL)
**HTML
JavaScript
CSS**
ASP / ASP.NET
JSP
PHP
DB
→ 필수 (웹 사이트를 만든다고 했을 때)

Python
Spring
Jquery
Ajax
→ 선택 (홈페이지보다 더 다양한 기술로 만들 떄)
```
- 웹을 만드는 기술은 아주 다양하나, 가장 일반적이고 기본적인 기술은 위의 것들이 있다.
<br>

### 1-1. HTML, JavaScript, CSS

>HTML - 웹 페이지를 채울 내용  
>JS - 웹 페이지에 들어갈 기능  
>CSS - 웹 페이지를 예쁘게 꾸밀 디자인  
<br>

- **HTML, JavaScript, CSS**는 클라이언트 쪽 페이지를 만드는 기술
- 이 기술들은 **웹을 만드는 표준**이자, **‘클라이언트 컴퓨터에서 동작하는 코드**(Client Side Script)’라는 공통점이 있다. 
- HTML, JavaScript, CSS는 **서버에 저장**되어 있고, 이를 웹 브라우저로 다운로드 받아서 **클라이언트 컴퓨터에서 실행**시킨다. 이때, 데이터를 받아오는 프로토콜이 ‘HTTP’이다.
- 즉, 웹 표준 데이터를 받아오는 애가 HTTP라고 생각하면 된다.
<br>

### 1-2. ASP/[ASP.NET](http://ASP.NET), JSP, PHP

- HTML, JavaScript, CSS와 다르게 **서버 컴퓨터에서 실행되는 기술** (서버 쪽 페이지를 만드는 기술)
- HTML, JavaScript, CSS처럼 다운을 받는 것뿐만 아니라 
프로그램 실행시키듯 **서버 쪽에서 실행이 되고, 그 결과만 보내준다.**
- ASP는 MS사에서 만들었으나 비주류 / 주로 자바 기반의 JSP를 쓴다. (어플, 웹, 공공기관 등)  
<br>
<br>

## 2. HTTP 프로토콜의 특징

- **HyperText Transfer Protocol(하이퍼 텍스트 전송 프로토콜)**
- www에서 쓰이는 핵심 프로토콜로 문서의 전송을 위해 쓰이며, 오늘날 거의 모든 웹 애플리케이션에서 사용되고 있다.
→ 음성, 화상 등 여러 종류의 데이터를 MIME로 정의하여 전송 가능

- **HTTP 특징** **: Request / Response(요청/응답)** 동작에  기반하여 서비스 제공

<br>

### 2-1. **HTTP 1.0**
<br>

- **HTTP 1.0의 특징**

    - **연결 수립, 동작, 연결 해제**의 **단순함**이 특징 → 하나의 URL은 하나의 TCP 연결
    - 즉, HTML 문서를 전송 받은 뒤 연결을 끊고 다시 연결하여 데이터를 전송한다.
    
     <br>

<img src="./캡처1.PNG" alt="Getting started" width="600" height="400">

<br>

- **HTTP 1.0의 문제점**

    - 단순 동작(연결 수립, 동작, 연결 해제)이 반복되어 통신 부하 문제 발생

    - HTTP 1.0의 경우, 클라이언트가 웹서버에 접속할 때 **TCP는 3 Way HandShake**를 한다.  
    → 그 후 HTTP 요청을 하고,응답을 한번 받으면 연결을 끊는다.  
    → 다시 연결을 받으려면 다시 3 Way HandShake를 하고 다시 HTTP를 요청해야 한다.
    - 예를 들어, 네이버 메인 페이지에 있는 그림 페이지가 10개라면, 메인 페이지와 연결하기 위해서는 10개의 그림 페이지를 받기 위해서 연결하고 데이터 받고 종료하는 과정을 10번 넘게 반복해야 함.  
    → 굉장히 **‘비효율적’**  
<br>    

<details>
<summary><Strong>TCP - 3 Way HandShake란?</strong></summary>
<div markdown="1">

- **TCP는 대용량의 데이터를 보내기 쉽게 작게 분해해서 상대에게 보내고, 정확하게 도착했는지 확인하는 역할을 담당한다.**
- **상대에게 데이터를 확실하게 보내기 위해서 TCP는 “3 Way HandShake”이라는 방법을 사용**
- **패킷을 보내고 나서 바로 끝내는 것이 아니라, 보내졌는지 여부를 상대에게 확인하러 간다.**
- 송신 측에서는 최초 ‘SYN’ 플래그로 상대에게 접속함과 동시에 패킷을 보내고,  
수신 측에서는 ‘SYN/ACK’ 플래그로 송신측에 접속과 동시에 패킷을 수신한 사실을 전한다.  
마지막으로 송신측이 ACK 플래그를 보내 패킷 교환이 완료되었음을 전한다.  
이 과정에서 어디선가 통신이 도중에 끊어지면 TCP는 그와 동시에 같은 수순으로 패킷을 재전송한다. 
> 출처 : <그림으로 배우는 Http & NetWork Basic>, p.27

</div>
</details>

<br>
<br>        

### 2-2. **HTTP 1.1**

- **HTTP 1.1의 특징 -** 1.0의 문제점을 보완함.
    - 한번 연결되면 끊지 않고 필요한 데이터 모두 받고 끊기는 방식
    - Multiple Request 처리가 가능하여 Client의 Request가 많을 경우 연속적인 응답 제공  
    → Pipeline 방식의 Request / Response 진행
    - HTTP 1.0과는 달리 Server가 갖는 하나의 IP Address와 다수의 Web Site 연결 가능
    - HTTP 1.0과 호환 가능
    - 빠른 속도와 Internet Protocol 설계에 최적화될 수 있도록 Cache 사용
    - Data를 압축해서 전달이 가능하도록 하여 전달하는 Data 양이 감소

<br>
<br>

# 3. HTTP 메소드

## 3-1. HTTP 요청 프로토콜의 구조
- 요청하는 방식을 정의하고, 클라이언트 정보를 담는다.
- 16진수가 아니라 영어와 특수문자를 쓴다.

| Request Line |
| --- |
| Headers |
| 공백 |
| Body |
<br>

- Header는 ‘여러 개의 옵션이 들어가는 개념’으로 이해하면 편하다.
- Body는 어떤 데이터를 요청할 때 보내는 추가적인 데이터  

<br>

### **HTTP 요청 프로토콜 예시**

<img src="./캡처2.PNG" alt="Getting started">

<br>

1. 첫번째 줄 - **리퀘스트 라인**

|  요청 타입 | 공백 |                          URI | 공백 |    HTTP 버전 |
| --- | --- | --- | --- | --- |
|      GET |  | produ/content.asp?code=sch-v310 |  |     HTTP/1.1 |
<br>
- 리퀘스트 라인은 이런 구조로 이루어진다. (중간의 띄어쓰기(공백)이 반드시 들어가야 함!)
- 요청 타입에 **HTTP 메소드**가 들어간다.

<br>

2. 두번째 줄 ~ Cookie까지 - ‘**헤더’**  

3. **공백**  

4. **Body** - Body는 항상 존재하는 것이 아니다. (위의 예시처럼 따로 보내는 데이터가 없을 수 있다)  
→ 요청 프로토콜에서 HTTP 버전은 대부분 똑같고, **요청 타입**과 **URI**가 아주 중요하다.

<br>
<br>

## 3-2. HTTP 메소드

<img src="./캡처3.PNG" alt="Getting started" width="600" height="400">

<br>

### **GET / POST**  **→ 중요**
- **GET**
    - 클라이언트가 서버에게 어떤 데이터를 **요청**하는 메소드
    - HTML, CSS, JavaScript 같은 웹페이지를 보내달라고 요청하는 것

    <br>

- **POST**
    - 클라이언트가 서버에게 어떤 데이터를 **전송**하는메소드    
    - 그런데, GET도 서버에게 데이터를 요청하면서 데이터를 전송할 수 있고,        
        POST도 서버에게 데이터를 전송하는 동시에 요청할 수 있다.        
        → 그렇다면 **GET / POST의 차이점은 무엇인가?  (아래의 에서 확인)**
        
    
    - GET / POST가 가장 일반적으로 사용하는 메소드이고, **나머지는 보안상 막을 수 있다.**
    
### **COPY / MOVE / DELETE** 
- 클라이언트가 서버에 있는 파일을 ‘복사 / 이동 / 삭제’하라고 요청하는 메소드
- 보안상 클라이언트는 서버 쪽에 있는 파일을 건드려서는 안되기 때문에, 이 메소드는 관리자가 대부분 막아 놓는다.

### **LINK / UNLINK / OPTION** 
- 링크를 생성, 삭제 / 사용 가능한 옵션(어떤 요청 파일이 사용 가능한지)을 알려주는 메소드
- 해킹의 첫 단계는 ‘정보를 수집’하는 것에서 시작되며, 보안이 취약해질 위험이 있으므로, 이 메소드도 관리자가 대부분 막아 놓는다.

### **PUT**
- 클라이언트가 서버 쪽에 어떤 자원(사진, 파일 등)을 업로드를 할 때 사용되는 메소드
- ‘업로드’는 PUT 메소드를 이용해서 클라이언트가 직접 업로드 하는 것이 아니라, 
JSP, ASP, PHP 같은 서버 프로그램을 통해 하는 것이 보통이다.
- PUT을 이용하면 무조건 업로드하는 것이기 때문에, 잘못하면 서버의 보안이 위험해짐.

<br>

## 3-3. GET / POST의 차이점 - ‘데이터를 서버로 보내는 방식’이 다르다.

> **GET** 방식은 **URI(주소창)**에 포함시켜서 보낸다.  
> 반면, **POST**는 **BODY**에 포함시켜서 보낸다.

<br>

- **GET의 경우**

<img src="./캡처6.PNG" alt="Getting started">

<br>

> **titleId=570503&weekday=thu**

    → titleId가 570503인 웹툰에, weekday가 목요일인 웹툰을 보여달라고 요청한 데이터
    → 이 부분에 보낼 데이터를 작성하는게 GET 방식
    → 주소창에 포함된다는 뜻은 **‘공개적’**으로 사람들이 볼 수 있다는 것이다.

<br>

- **POST 프로토콜 예시**

<img src="./캡처5.PNG" alt="Getting started" width="600" height="400">


<br>

> **uid = ———— & upw = ————** 

    → POST는 BODY에 포함하여 보내기 때문에, ‘패킷 캡쳐’를 하지 않으면 볼 수 없다.  
    → GET보다는 비교적 덜 공개적.

<br>

### **정리**
- GET, POST 메소드 모두 데이터 전송과 요청이 가능하다.
- 그러나 **GET은 주소창에 보이는 공개적인 방식**으로 전송하기 때문에, 비교적 중요하지 않은 데이터를 보냄.
- **POST는 BODY에 숨겨서 보내는 방식**으로, **비교적 덜 공개적**이기 때문에 아이디, 패스워드 같이 중요한 정보를 보낸다.
- 그러나 POST라고 완전히 안전하진 X / 따라서 이러한 **취약점을 보완한 HTTPS**를 써야 한다.
- 대부분의 사이트가 최소한 ‘로그인’할 때는 HTTPS를 쓰는 것을 확인할 수 있다.