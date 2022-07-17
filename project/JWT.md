## JWT
Json Web Token

전자로 서명 된 URL-safe JSON(URL로 이용할 수 있는 문자만으로 구성)
* 속성 정보(Claim)를 JSON 데이터 구조로 표현한 토큰
* RFC7519 표준
* Server와 Client 간 정보를 주고 받을 때 http request header에 JSON Token을 넣은 후 Server는 별도의 인증 과정없이 header에 포함된 JWT정보를 통해 인증
* 이 때 사용되는 JSON 데이터는 URL에 포함할 수 있는 문자로만
	* URL-Safe하게 하기 위함
* HMAC Algorithm을 사용하여 비밀키 혹은 RSA을 이용한 Public Key / Private Key 쌍으로 서명할 수 있다.

### JWT Token의 구성
3개의 파트로 나눠져 있다.

aaaaaa.bbbbbb.cccccc 형식으로 표현
헤더(Header), 페이로드(Payload), 서명(Signature)로 구성
* Base64 인코딩의 경우 "+", "/", "="이 포함되지만 JWT는 URI에서 파라미터로 사용할 수 있도록 URL-Safe한 Base64url인코딩을 사용

Header
토큰의 타입과 해시암호화 알고리즘으로 구성
1. 토큰의 유형(JWT)
2. HMAC.SHA256 또는 RSA와 같은 Hash Algorithm

Payload
토큰에 담을 클레임정보(Claim)를 포함
정보의 한 '조각'을 클레임이라고 하며 이는 name/value의 한 쌍으로 이루어진다.
토큰에는 여러 개의 클레임을 넣을 수 있다.
클레임의 종류
* 등록된 클레임(registerd)
* 공개 클레임(public)
* 비공개 클레임(private)

Signature
sercret key을 포함하여 암호화되어 있다.

### Process
Browser(Client, 사용자), Server(서버)
1. Browser가 username(id)와 password을 입력하여 로그인 request
2. Server가 request을 확인하고 secret key을 통해 Access Token 발급
3. JWT Token을 Client에 전달
4. Client에서 API을 request할 때 Client가 Authorization header에 Access token을 담아서 request
5. Server은 JWT Signature을 확인하고 Payload로부터 사용자 정보를 확인하고 데이터를 반환
6. Client의 로그인 정보를 Server memory에 저장하지 않기 때문에 Token 기반 인증 메커니즘을 제공


### API
**Signup API**

POST/auth/signup

✔Request Data
* uid: 회원가입 할 계정에 대한 id
* password: 회원가입 할 계정에 대한 비밀번호
* role: 회원가입 할 계정에 대한 역할
* position: 회원가입 할 계정에 대한 포지션

✔Response Data
* status: 200
* message: Success
* data: {}

**Signin API**

POST/auth/signin

✔Request Data
* uid: 회원가입에서 기재한 id 정보
* password: 회원가입에서 기재한 비밀번호 정보

✔Response Data
* status
* data
	* uid: 회원가입에서 기재한 id 정보
	* role: 회원가입에서 기재한 대한 역할의 정보
	* position: 회원가입에서 기재한 포지션에 대한 정보
	* accessToken: 엑세스 토큰에 대한 정보
	* refreshToken: 리프레시 토큰에 대한 정보
* message: User information matched

**identification API**

GET/auth/me

✔Response Data
* status
* data
	* uid: 회원가입에서 기재한 id 정보
	* upk: 회원가입에서 기재한 임의로 부여된 계정에 대한 Primary key
	* role: 회원가입에서 기재한 대한 역할의 정보
	* position: 회원가입에서 기재한 포지션에 대한 정보
	* iat
	* exp
* message: "Success"

**reissue access token API**

GET/auth/me

✔Response Data
* status: 200
* message: Sucess
* data
	* accessToken: "재갱신된 access token 정보"

🎯position와 role은 권한 체크를 할 때 사용한다.

❗accessToken와 refreshToken
**accessToken**

자원에 접근할 수 있는 Token

**refreshToken**

accessToken을 계속 갱신 받는 것이 주 목적

로그인을 한 후 두 Token을 cookie에 저장
👉원하는 Token에 대한 핸들링을 구현

❗
iss: Token 발급자(issuer)

sub: Token 제목(subject)

aud: Token 대상자(audience)

exp: Token의 만료시간(expiration), 시간은 NumericData 형식(현재시간 이후로 설정)

nbf: Not Before을 의미, Token의 활성 날짜와 유사한 개념

iat: Token이 발급된 시간(issued at), 이 값을 통해 토큰의 age를 판단 가능

jti: JWT의 고유식별자, 중복적인 처리를 방지하기 위해 사용(일회용 토큰 사용 시 유용하다.)


📝

Navigation Gaurd을 통해 url이 변경될 때마다 Token을 Check

Component가 변경될 때마다 Token을 Check

axios가 발생할 때마다 interceptor을 이용하여 Token을 Check
```vue
import VueCookies form 'vue-cookies';
```