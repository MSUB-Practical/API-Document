# 인증번호 API

인증번호 API는 기업, 학생 개발자를 위한 메일, 문자 전송 API입니다.

## ResultCode

- `0` | 호출 성공
- `1` | 매개변수가 비어있음
- `2` | 이미 존재하는 ID
- `3` | 유저를 찾을 수 없음
- `4` | 찾을 수 없는 타입
- `5` | 문자 또는 메일을 전송하지 못함
- `6` | 그 외 에러

## Response 유형

```jsx
{
	"code": (int) ResultCode,
	"message": "some message",
	"result": array|object|null // 이 밑에서 설명하는 Response랑 같음
}
```

서버 주소 - http://mist.pw:30012

### POST /signup

- 서비스를 이용을 위한 회원가입
- Request
    
    ```jsx
    POST /signup HTTP/1.1
    Content-Type: application/json
    
    {
    	"id": string,    // 사용자 ID
    	"pw": string,    // 사용자 비밀번호
    	"name": string,  // 사용자 이름
    	"email": string  // 사용자 이메일
    }
    ```
    

### POST /login

- 서비스 로그인
- Request
    
    ```jsx
    POST /login HTTP/1.1
    Content-Type: application/json
    
    {
    	"id": string,   // 사용자 ID
    	"pw": string    // 사용자 비밀번호
    }
    ```
    
- Response
    
    ```jsx
    result: {
    	"id": string,    // 사용자 ID
    	"name": string,  // 사용자 이름
    	"email": string, // 사용자 이메일
      "token": string  // 유저 토큰
    }
    ```
    

### POST /userinfo

- 토큰을 통한 사용자 정보 불러오기
- Request
    
    ```jsx
    POST /userinfo HTTP/1.1
    Content-Type: application/json
    
    {
    	"token": string // 사용자 토큰
    }
    ```
    
- Response
    
    ```jsx
    result: {
    	"id": string,         // 사용자 ID
    	"pw": string,         // 사용자 비밀번호
    	"name": string,       // 사용자 이름
    	"email": string,      // 사용자 이메일
    	"data": [
    		{
    			"to": string,     // 받는 사람의 전화번호 또는 메일
    			"text": string,   // 보낸 메시지의 내용
    			"date": Date,     // API를 호출한 날짜
    			"successed": bool // API 성공 여부
    		}
    	]
    }
    ```
    

### POST /message

- 문자 메시지 전송
- Request
    
    ```jsx
    POST /message HTTP/1.1
    Content-Type: application/json
    
    {
    	"to": string,   // 받는 사람의 메일
    	"text": string, // 보낼 메시지의 내용
    	"token": string // 사용자 토큰
    }
    ```
    

### POST /mail

- 메일 전송
- Request
    
    ```jsx
    POST /mail HTTP/1.1
    Content-Type: application/json
    
    {
    	"to": string,    // 받는 사람의 메일
    	"text": string,  // 보낼 메시지의 내용, html 태그 사용 가능
    	"title": string, // 보낼 메일의 제목
    	"token": string  // 사용자 토큰
    }
    ```
    

### POST /today

- 하루 사용량 불러오기
- Request
    
    ```jsx
    POST /today HTTP/1.1
    Content-Type: application/json
    
    {
    	"year": string|number,  // 확인할 날의 연도
    	"month": string|number, // 확인할 날의 월
    	"date": string|number   // 확인할 날의 일
    	"token": string         // 사용자 토큰
    }
    ```
    
- Response
    
    ```jsx
    result: [
    	{
    		"to": string,     // 받는 사람의 전화번호 또는 메일
    		"text": string,   // 보낸 메시지의 내용
    		"date": Date,     // API를 호출한 날짜"
    		"successed": bool // API 성공 여부
    	}
    ]
    ```
    

### POST /month

- 월 사용량 불러오기
- Request
    
    ```jsx
    POST /month HTTP/1.1
    Content-Type: application/json
    
    {
    	"year": string|number,  // 확인할 날의 연도
    	"month": string|number, // 확인할 날의 월
    	"token": string         // 사용자 토큰
    }
    ```
    
- Response
    
    ```jsx
    result: [
    	{
    		"to": string,     // 받는 사람의 전화번호 또는 메일
    		"text": string,   // 보낸 메시지의 내용
    		"date": Date,     // API를 호출한 날짜"
    		"successed": bool // API 성공 여부
    	}
    ]
    ```
