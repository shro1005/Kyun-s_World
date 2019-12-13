---
description: 'HTTP의 기초인 메소드와 URL , 헤더, 바디, 스테이터스 코드'
---

# HTTP/0.9 ~ HTTP/1.0 \(HTTP의 기초 1 - 메소드와 경로, 스테이터스 코드\)

HTTP의 기본 요소를 아래 5가지로 정리할 수 있다. \(실제 책에서는 메소드와 경로를 하나로 합쳤지만 필자 나누고 싶다.\)

1. **메소드**
2. **경로**
3. **헤더**
4. **바디**
5. **스테이터스 코드** 

위 내용을 정리해 봤다.

## 1. 메소드 

메드의 경우 HTTP/0.9에서는 실현되지 않았고, 뉴스그룹\(유즈넷\)이라는 플랫폼에서 부터 도입되어 HTTP/1.0 등장했다. 1.1로 버전이 바뀌면서 사라진 메서드도 존재하고, 추가로 등록된 메서도 있다고 한다. 

아래 내용은 2018년 기준 HTTP/1.1 버전의 메드 목록이다. \([https://www.yeahhub.com/list-http-methods-2018-update/](https://www.yeahhub.com/list-http-methods-2018-update/) 를 참고하여 작성했다.\)

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#xBA54;&#xB4DC; &#xBA85;</b>
      </th>
      <th style="text-align:left"><b>&#xC804;&#xC1A1;&#xC2DC; &#xAD6C;&#xC870; (&#xBB38;&#xBC95;)</b>
      </th>
      <th style="text-align:left"><b>&#xC124;&#xBA85;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>GET</b>
      </td>
      <td style="text-align:left">
        <p>GET &lt;Request URI&gt;?query_string HTTP/1.1\r\n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt; r\n\r\</p>
      </td>
      <td style="text-align:left">
        <p>&#xC9C0;&#xC815;&#xB41C; Request-URI&#xC5D0;&#xC788;&#xB294; &#xC790;&#xC6D0;&#xC5D0;
          &#xC758;&#xD574; &#xC800;&#xC7A5;&#xB418;&#xAC70;&#xB098; &#xC0DD;&#xC131;
          &#xB41C; &#xAC83;&#xC744; &#xAC80;&#xC0C9;&#xD558;&#xB294; &#xB370; &#xC0AC;&#xC6A9;&#xB41C;&#xB2E4;.
          &#xBC84;&#xC758; &#xD574;&#xB2F9; &#xC790;&#xC6D0;&#xC740; &#xB370;&#xC774;&#xD130;&#xB97C;
          &#xC218;&#xC2E0;&#xD558;&#xC5EC; &#xC0AC;&#xC6A9; &#xBC0F; &#xC0C1;&#xD638;&#xC791;&#xC6A9;
          &#xD560; &#xC218; &#xC788;&#xB2E4;.</p>
        <p>GET&#xC73C;&#xB85C; &#xC124;&#xC815;&#xD558;&#xC5EC; HTML &#xC591;&#xC2DD;
          &#xBCC0;&#xC218;&#xB97C; &#xC81C;&#xCD9C;&#xD558;&#xBA74; &#xB9E4;&#xAC1C;
          &#xBCC0;&#xC218;&#xAC00; &#xC870;&#xD68C; &#xBB38;&#xC790;&#xC5F4;&#xB85C;
          &#xC778;&#xCF54;&#xB529;&#xB418;&#xC5B4; GET &#xC694;&#xCCAD; &#xBA54;&#xC18C;&#xB4DC;&#xB97C;
          &#xC0AC;&#xC6A9;&#xD558;&#xC5EC; Request-URI&#xC758; &#xC77C;&#xBD80;&#xB85C;
          HTTP &#xC11C;&#xBC84;&#xC5D0; &#xC81C;&#xCD9C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>POST</b>
      </td>
      <td style="text-align:left">
        <p>POST &lt;Request URI&gt; HTTP / 1.1 r n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt; r n
          <br />Content-Length: &lt;length in bytes&gt;\r\n
          <br />Content-Type: &lt;content type&gt;\r\n\r\n</p>
        <p>&lt;Request URI&#xC5D0; &#xC804;&#xB2EC;&#xD560; query_string &#xB610;&#xB294;
          &#xB370;&#xC774;&#xD130;&gt;</p>
      </td>
      <td style="text-align:left">
        <p>&#xC9C0;&#xC815;&#xB41C; Request-URI&#xC5D0;&#xC788;&#xB294; &#xC790;&#xC6D0;&#xC5D0;
          &#xB370;&#xC774;&#xD130;&#xB97C; &#xC81C;&#xCD9C;&#xD558;&#xB294; &#xB370;
          &#xC0AC;&#xC6A9;&#xB41C;. &#xC11C;&#xBC84;&#xC758; &#xD574;&#xB2F9; &#xC790;&#xC6D0;&#xC740;
          &#xB370;&#xC774;&#xD130;&#xB97C; &#xC218;&#xC2E0;&#xD558;&#xC5EC; &#xC0AC;&#xC6A9;
          &#xBC0F; &#xC0C1;&#xD638;&#xC791;&#xC6A9; &#xD560; &#xC218; &#xC788;&#xB2E4;.</p>
        <p>POST&#xB85C; &#xC124;&#xC815;&#xB41C; HTML &#xC591;&#xC2DD; &#xBCC0;&#xC218;&#xAC00;
          &#xC81C;&#xCD9C;&#xB418;&#xBA74; &#xB9E4;&#xAC1C; &#xBCC0;&#xC218;&#xAC00;
          POST &#xC694;&#xCCAD; &#xBA54;&#xC2DC;&#xC9C0;&#xC758; &#xBCF8;&#xBB38;&#xC73C;&#xB85C;
          &#xC778;&#xCF54;&#xB529;&#xB418;&#xC5B4; HTTP &#xC11C;&#xBC84;&#xC5D0;
          &#xC81C;&#xCD9C;&#xB41C;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HEAD</b>
      </td>
      <td style="text-align:left">
        <p>HEAD &lt;Request-URI&gt; HTTP/1.1\r\n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt;\r\n\r\n</p>
      </td>
      <td style="text-align:left">
        <p>HTTP 1.1 &#xC11C;&#xBC84;&#xAC00; &#xC751;&#xB2F5;&#xC5D0;&#xC11C; &#xCF58;&#xD150;&#xCE20;&#xB97C;
          &#xB9AC;&#xD134;&#xD558;&#xC9C0; &#xC54A;&#xC544;&#xC57C;&#xD55C;&#xB2E4;&#xB294;
          &#xC810;&#xC744; &#xC81C;&#xC678;&#xD558;&#xACE0; GET &#xBA54;&#xC18C;&#xB4DC;&#xC640;
          &#xB3D9;&#xC77C;&#xD558;&#xB2E4;.</p>
        <p>&#xC751;&#xB2F5;&#xC73C;&#xB85C; HTTP &#xD5E4;&#xB354;&#xC5D0; &#xD3EC;&#xD568;
          &#xB41C; &#xBA54;&#xD0C0; &#xC815;&#xBCF4;&#xB294; GET &#xC694;&#xCCAD;&#xC5D0;
          &#xB300;&#xD55C; &#xC751;&#xB2F5;&#xC73C;&#xB85C; &#xC804;&#xC1A1; &#xB41C;
          &#xC815;&#xBCF4;&#xC640; &#xB3D9;&#xC77C;&#xD574;&#xC57C; &#xD558;&#xBA70;,
          &#xC11C;&#xBC84;&#xC5D0; &#xB300;&#xD55C; &#xBA54;&#xD0C0; &#xC815;&#xBCF4;&#xB97C;
          &#xC5BB;&#xB294; &#xB370; &#xC0AC;&#xC6A9;&#xD560; &#xC218; &#xC788;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PUT</td>
      <td style="text-align:left">
        <p>PUT &lt;Request-URI&gt; HTTP/1.1\r\n
          <br />Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt;\r\n
          <br />Content-Length: &lt;length in bytes&gt;\r\n
          <br />Content-Type: &lt;content type&gt;\r\n\r\n</p>
        <p>&lt;&#xD30C;&#xC77C;&#xC5D0; &#xCCA8;&#xBD80;&#xD560; &#xB370;&#xC774;&#xD130;e&gt;</p>
      </td>
      <td style="text-align:left">
        <p>&#xB370;&#xC774;&#xD130;&#xB97C; HTTP &#xC11C;&#xBC84;&#xB85C; &#xC804;&#xC1A1;&#xD558;&#xACE0;
          Request-URI&#xB85C; &#xC2DD;&#xBCC4;&#xB418;&#xB294; &#xC704;&#xCE58;&#xC5D0;
          &#xC800;&#xC7A5;&#xD560; &#xC218; &#xC788;&#xB2E4;.</p>
        <p>(<a href=" https://www.yeahhub.com/http-put-method-exploitation-live-penetration-testing/">&#xD65C;&#xC6A9; &#xCC38;&#xACE0;</a>)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">OPTIONS</td>
      <td style="text-align:left">
        <p>OPTIONS &lt;Request-URI&gt; HTTP/1.1\r\n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt;\r\n\r\n</p>
      </td>
      <td style="text-align:left">Request-URI&#xB85C; &#xC2DD;&#xBCC4; &#xB41C; &#xC694;&#xCCAD; / &#xC751;&#xB2F5;
        &#xCCB4;&#xC778;&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;&#xD55C;
        &#xD1B5;&#xC2E0; &#xC635;&#xC158;&#xC5D0; &#xB300;&#xD55C; &#xC815;&#xBCF4;
        &#xC694;&#xCCAD;&#xC744; &#xB098;&#xD0C0;&#xB0B8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">DELETE</td>
      <td style="text-align:left">
        <p>DELETE &lt;Request-URI&gt; HTTP/1.1\r\n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt;\r\n\r\n</p>
      </td>
      <td style="text-align:left">&#xC624;&#xB9AC;&#xC9C4; &#xC11C;&#xBC84;&#xAC00; Request-URI&#xB85C;
        &#xC2DD;&#xBCC4; &#xB41C; &#xC790;&#xC6D0;&#xC744; &#xC0AD;&#xC81C;&#xD558;&#xB3C4;&#xB85D;
        &#xC694;&#xCCAD;&#xD55C;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">TRACE</td>
      <td style="text-align:left">
        <p>TRACE &lt;Request-URI&gt; HTTP/1.1\r\n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt;\r\n\r\n</p>
      </td>
      <td style="text-align:left">
        <p>&#xC694;&#xCCAD; &#xBA54;&#xC2DC;&#xC9C0;&#xC758; &#xC6D0;&#xACA9; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
          &#xACC4;&#xCE35; &#xB8E8;&#xD504;&#xBC31;&#xC744; &#xD638;&#xCD9C;&#xD558;&#xB294;
          &#xB370; &#xC0AC;&#xC6A9;&#xB41C;&#xB2E4;.</p>
        <p>&#xD074;&#xB77C;&#xC774;&#xC5B8;&#xD2B8;&#xB294; &#xC694;&#xCCAD; &#xCCB4;&#xC778;&#xC758;
          &#xB2E4;&#xB978; &#xCABD; &#xB05D;&#xC5D0;&#xC11C; &#xC218;&#xC2E0;&#xB418;&#xB294;
          &#xB0B4;&#xC6A9;&#xC744;&#xBCF4;&#xACE0; &#xD574;&#xB2F9; &#xB370;&#xC774;&#xD130;&#xB97C;
          &#xD14C;&#xC2A4;&#xD2B8; &#xBC0F; &#xC9C4;&#xB2E8; &#xC815;&#xBCF4;&#xB85C;
          &#xC0AC;&#xC6A9;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CONNECT</td>
      <td style="text-align:left">
        <p>CONNECT &lt;Request-URI&gt; HTTP/1.1\r\n</p>
        <p>Host: &lt;&#xD638;&#xC2A4;&#xD2B8;&#xC758; &#xD638;&#xC2A4;&#xD2B8; &#xC774;&#xB984;
          &#xB610;&#xB294; IP &#xC8FC;&#xC18C;&gt;\r\n\r\n</p>
      </td>
      <td style="text-align:left">Request-URI&#xB85C; &#xC2DD;&#xBCC4; &#xB41C; &#xC790;&#xC6D0;&#xC5D0;
        &#xB300;&#xD55C; &#xD504;&#xB85D;&#xC2DC; &#xC5F0;&#xACB0;&#xC744; &#xC9C0;&#xC815;&#xD558;&#xB294;
        &#xB370; &#xC0AC;&#xC6A9;&#xB41C;&#xB2E4;.</td>
    </tr>
  </tbody>
</table>

가장 흔히 사용되는 메소드는 GET, POST, HEAD 로 간략하게 정리하면 아래와 같다.

* GET : 서버에 헤더와 콘텐츠를 요청
* POST : 새로운 문서 투고 \(뉴스그룹에서 처럼\)
* HEAD : 서버에 헤더만 요청

## 2. 경로

경로는 HTTP/0.9에서도 사용된 요소로 클라이언트가 서버로 요청을 보낼때 사용한다.                             

경로는 URL에 포함되는 내용이다. 문서에서는 URI와 URL이 모두 등장하지만, 우리에겐 URL이 더 익숙할 것이다. 사실 URI의 일부로 URL이 등장했지만, 웹 시스템을 다루는 한 URI와 URL은 거의 같다고 보기 때문에 이후부터는 URL로 말하겠다.

\(프로그래밍 언어에서도  루비, C\#은 URI를  Go 언어와 파이썬, Node.js는 URL을 사용하며, Java는 URI, URL 클래스를 모두 가지고 있다.\)

일반적으로 URL의 구조는 아래와 같다. \(구글을 예시로 하지만 실제 존재하는 URL은 아닙니.\)

> https://www.google.com/search.html?contents=http

여기서  분해를 하면 다음과 같다.

* https:  :   **스키마**
* www.google.com  :  **호스트명**
* search.html?contents=http  :  **경로**

위에서 메소드 목록의 전송시 문법에서도 이를 확인할 수 있다.

> GET &lt;Request URI&gt;?query\_string HTTP/1.1\r\n 
>
> Host: &lt;호스트의 호스트 이름 또는 IP 주소&gt;  r\n\r\

 여기서 &lt;Request URI&gt;?query\_string 에 해당되는 부분이 경로이다.

**경로는 즉 집에 있는 '방'이라고 할 수 있다. URL이 '주소'라고 하면 호스트는 '집'  경로는 '방' 이라고 할 수 있다. 같은 집이라도 다른 방에 들어가면 다른 사람이 반기는 것과 같은 느낌이다.**

그렇다면 저자가 URL 대신 경로를  HTTP의 기본 요소에 포함시킨 이유는 무엇일까?                                                        

그 이유는 **서버에서 받아들이는 것은 경로 뿐**이기 때문이라고 필자는 생각한다. 실제로 웹 개발 시 컨트롤러에서 request mapping을 할때 호스트 명은 사용하지 않고 경로부분만 사용한다.  

## 3. 스테이터스 코드

만약 잘못된 경로로 요청을 보냈거나, 다른 이유들로 우리가 보낸 요청이 잘 못됐다는 것을 알기 위해선 응답이 필요하다. 이런 응답을 한눈에 알 수 있게 하는 것이 스테이터스 코드이다.

스테이터스 코드도 경로와 마찬가지로 뉴스그룹에서 가져온 기능이다. 

404에러, 503에러등 익숙한 그 에러들이 이 스테이터스 코드에 속한다. 스테이터스 코드는 크게 다섯가지 카테고리로 나눌수 있다.

* 100번대 : 처리가 진행중임을 나타내는 코드로, 100번대 계열은 특수한 용도로 사용되며, 이후에 다루도록 하겠다ㅏ.
* 200번대 : 가장 기쁜 코드다. 바로 성공했을 때의 응답.
* 300번대 : 서버에서 클라이언트로 보내는 명령이다. 오류가 아니라 정상 처리 범주에 속하며, 가장 익숙한 것을 리다이렉트 등이 있다.
* 400번대 : 클라이언트가 보낸 요청에 오류가 있다는 내용이다.
* 500번대 : 서버에서 오류가 있다는 것을 알리는 내용이다.

각 카테고리 안에서도 다양한 코드들이 있는데 자세한 내용은 아래 링크를 통해 확인할 수 있다.

\( [자세한 스테이터스 코드 내용  ](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)\)

## 4. 바디

바디 역시 HTTP/0.9에서 사용됐다. HTTP/0.9는 정말 단순하게 '브라우저가 요청시, 서버에서는 데이터를 돌려준다'라는 기능만 제공했다. 따라서  HTTP/0.9에서는 요청할 경로와 수신받을 데이터인 바디만 존재했다.

\(브라우저의 요청에 응답하는 데이터라면 HTML, JSON, 이미지 등 이 될수 있다.\) 

그렇다면 클라이언트에서 요청을 보낼 때 서버에 특정한 데이터를 주고 싶은 경우는 어떡할까? 그래서 HTTP/1.0부터 요청시 서버로 데이터를 전송 할 수 있도록 송신 바디가 생겼다. \(송신 바디 역시 JSON이 될 수 있고 바이너리 데이터 등이 될 수 있다.\)

다만 GET 메소드의 경우  송신 바디를 보내지 않는 것이 원칙이다. 책에서는 GET 메소드의 경우도 바디를 존송 할 수 있지만 그닥 추천하지 않는 다고 나와있다. 그러니 단순한 페이지 이동이나 경로에 줄 수 있는 query string을 제외한 다른 데이터들을 서버로 요청시 전달 하고 싶다면 다른 메소드를 사용하는 것이 좋다.

## 5. 헤더





