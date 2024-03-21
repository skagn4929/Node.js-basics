# Node.js 백엔드 기초
- [Node.js 백엔드 기초 (ft.API 구축)](https://www.youtube.com/watch?v=Tt_tKhhhJqY&t=2905s)

해당 영상을 통해 Node.js 기초를 학습하고 정리한 내용입니다.

## Node.js ?
- 브라우저에서 실행되는 자바스크립트를 컴퓨터나 서버에서 실행할 수 있도록 해주는 플랫폼   
- 모듈 기능과 npm 패키지 매니저를 통해 미리 짜여진 코드를 활용하여 개발 속도를 높일 수 있다.

## Visual Studio Code를 이용해 Node.js 환경에서 'hello world' 출력
- VSC 실행 후 프로젝트 폴더를 열어서 index.js 파일을 생성
- Node.js를 이용해 `console.log("hello world")` 출력 테스트
- 터미널에서 `node index.js` 명령어로 서버를 실행하고, 출력 결과를 확인

## npm ?
- 모듈을 설치하고 관리하는 패키지 매니저
- npm에서는 프로젝트를 위해 필요한 많은 모듈을 제공하며, 프레임워크나 라이브러리를 가져와서 사용할 수 있다.
- 모든 모듈을 직접 구현하지 않아도 되며, 필요한 모듈이 있다면 npm을 통해 검색하고 가져와서 사용하면 된다.
- 노드를 이용할 때에는 터미널에서 `npm install` 명령어를 입력하여 설치 후 사용할 수 있다.

## express 모듈
- Node.js 환경에서 웹 프레임워크를 만들기 위한 것이며, 프런트엔드에서 백엔드로 요청을 보내고, 그것을 처리하는 등의 역할을 한다.
- `npm install express`로 설치 후 usage를 입력하고 실행하면 locallhost:3000 포트에서 Hello World!가 출력 된 것을 볼 수 있다.
> 모듈 삭제 : `npm uninstall (모듈)`   
> 서버 종료 : Ctrl + C

## HTTP 메서드, 라우팅, 콜백 함수의 개념
```jsx
// 예제)

app.get('/', (req, res) => {
	res.send('Hello World!')
})

// HTTP 메서드 : get
// 라우팅 : '/'
// 콜백 함수 : () => {}
```
- HTTP 메서드 : 요청의 목적, 종류를 알려주기 위해 사용하는 수단
> GET : 주소창에서 데이터 전달, params와 query로 받을 수 있다.   
> POST : 주소창 x, 내부적으로 body에 데이터 전달

- 라우팅 : 서버 내에서 특정 포트에 접근할 때 다양한 페이지를 제공하는 것을 의미한다.

- 콜백 함수 : 다른 코드의 인수로서 넘겨주는 실행 가능한 코드
> 앞에 적힌 함수 먼저 실행 후에 그다음에 실행할 함수 = 콜백 함수

## 예제 API 만들어보기
- GET/dog => {'sound': '멍멍'}
```jsx
app.get('/dog', (req, res) => {
	res.json({'sound': '멍멍'})
})
```
- GET/cat => {'sound': '야옹'}
```jsx
app.get('/cat', (req, res) => {
	res.json({'sound': '야옹'})
})
```

## 동물 소리 API 서버 만들기
- GET/sound/:name
- name에 따라서 다른 소리를 구현
```jsx
app.get("/sound/:name", (req, res) => {
  const { name } = req.params;

  if (name === "dog") {
    res.json({ sound: "멍멍" });
  } else if (name === "cat") {
    res.json({ sound: "야옹" });
  } else if (name === "pig") {
    res.json({ sound: "꿀꿀" });
  } else {
    res.json({ sound: "알수없음" });
  }
});
```

## CORS 이슈
HTML 파일로 서버에 요청했을 때 보안상 기본적으로 막게 되는데 CORS 설정을 통해 응답이 잘 되도록 만들어주는 게 필요하다.
- `npm install cors` 명령어로 cors 모듈 설치
```jsx
var cors = require('cors')

app.use(cors())
```
