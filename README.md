# NomadCoder NextJS 14ver 강의

## 2.3 SSR vs CSR

먼저 렌더링에 대해 알아보자

1. 렌더링이란 ?
   - NextJS가 리액트 컴포넌트를 브라우저가 이해할 수 있는 HTML로 변환하는 작업
2. SSR이란 ?
   - Server Side Rendering
   - 서버에서 페이지를 그려 클라이언트(브라우저)로 보낸 후 화면에 표시
   - NextJS로 웹 사이트를 빌드할 때, 기본적으로 SSR을 사용
3. CSR이란 ?
   - Client Side Rendering
   - 모든 렌더링이 클라이언트(브라우저) 측에서 발생
   - 클라이언트는 자바스크립트를 로드 -> 자바스크립트가 UI를 빌드

## 2.4 Hydration

nextJS에서는 Hydration은 단순 HTML을 React apllication으로 초기화 하는 작업이다.

SSR을 통해 만들어진 interactive하지 않는 HTML을 클라이언트 측에서 interactive하게 리액트 컴포넌트로 변화하는 과정이다.<br/>
(HTML에게 영양소를 지급한다고 생각해보자)

홈페이지 접속 -> 지루한 HTML을 보여줌 -> 일단 사용자들은 화면이 보이기에 좋음
<br/>-> 보는 사이에 HTML에게 기능들을 장착중!!!
