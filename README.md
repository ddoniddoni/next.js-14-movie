# NomadCoder NextJS 14ver 강의

## Link => [Vercel 배포 링크](https://next-js-14-movie-seven.vercel.app/)

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

## 2.5 'use client'

'use client'를 맨 상단에 입력한 Component는 이렇게 말한다.
<br/>"이봐! 이 component는 client에서 interactive해야 해!, 이 컴포넌트는 hydrated 되어야 해"

use client를 선언하지 않으면 기본적으로 모두 server component가 된다.<br/>
"use client"은 서버와 클라이언트 컴포넌트 모듈 간의 경계를 선언하는 데 사용됩니다.
즉, 파일에 "use client"을 정의하면 하위 컴포넌트를 포함하여 해당 파일로 가져온 다른 모든 모듈이 클라이언트 번들의 일부로 간주됩니다.

## 2.7 Layouts

React 모델을 사용하다보면 페이지를 컴포넌트로 분해할 수 있는데, 재사용 되는 컴포넌트들이 많다 <br/>
ex) 네비게이션 바, 푸터 등 <br/>
이걸 layout화 해서 어떤 페이지에서든지 네비게이션바와 푸터가 존재한다.

## 2.8 metadata

page나 layout만 메타데이터를 보낼 수 있다. 즉 서버 컴포넌트에만 있을 수 있다.
<br/>
Next.js에는 향상된 SEO 및 웹 공유성을 위해 애플리케이션 메타데이터(ex: HTML head 엘리먼트 내의 meta 및 link 태그)를 정의하는 데 사용할 수 있는 메타데이터 API가 있습니다.

## 2.9 Dynamic Routes

Dynamic Routes는 /home, /about-us처럼 정적인게 아니라
<br/>id값이나 uuid가 /about-us/[id or uuid]가 있는 것이다.
<br/>폴더명을 [id]처럼 만들어준다.
<br/>ex) /app/movies/[id]/page.tsx

## 3.1 Client side

useState를 사용하는 순간, nextjs에서는 해당 page에 'use client'를 선언해줘야 한다.
<br/>그러면 metadata를 사용할 수 없다.
<br/>그리고 기존 react 방식의 fetch가 아닌 nextJS의 fetch를 사용해보자

## 3.2 Server Side

이전 fetch는 데이터를 받아오는동안 loading이 생겨서 사용자에게 화면이 보이지 않았다.
<br/>하지만 Next.js는 기본 웹 fetch() API를 확장하여 서버의 각 요청이 자체 영구 캐싱 의미를 설정할 수 있도록 한다.

## 3.3 Loading Component

해당 페이지 디렉토리 안에 loading.tsx 파일을 만들어 두면
<br/>데이터를 가져오는 동안 Loading중일때 알아서 화면을 보여줌
<br/>그래서 사용자는 로딩되고 있다는걸 알 수 있음.
<br/>
<br/>react suspense를 loading.js로 사용해서 의미 있는 로딩 UI를 만드는데 도움이 된다.
<br/>스켈레톤 및 스피너 같은 표시로 사전 렌더링이 가능하다.
<br/>사용자는 앱이 응답하고 있음을 이해할 수 있다.

## 3.4 Parallel Requests

fetch가 오래 걸리는 작업이 있으면
<br/>ex) getMovie, getVideos가 있을 때 getMovie가 20초 걸리고 getVideos가 0.5초 걸려도 총 20초 뒤에 getVideos를 구하게 된다
<br/>그럼 너무 오래걸리기 때문에 Parallel Request가 있어야 한다.
<br/>그래서 Promise.all을 사용한다.
<br/>ex) const [movie, videos] = await Promise.all([getMovie(id), getVideos(id)]);

## 3.5 Suspense

Promise.all을 사용해도 묶인 함수가 둘 다 끝나야만 데이터를 가져올 수 있다.
<br/>병렬적으로 진행한다 해도 Promise.all 같은 경우 같이 시작했을 때 둘 다 끝나야 값을 가질 수 있다.
<br/>한쪽만 데이터를 다 가져왔지만 한쪽이 로딩중이면 데이터가 다 나오지 않는것이다.
<br/>이걸 해결하기 위해 Suspense를 사용한다.
<br/>Suspense가 데이터를 fetch하기 위해 이 안의 component를 await하는 중.

## 3.7 Error Handling

하나의 페이지는 잘 작동하지 않을 수 있지만, 전체 웹이 오류에서 벗어나지 못하면 안된다.
<br/>디렉토리안에 error.js(jsx) 파일을 작성하면 해당 페이지않에 error가 발생했을 때
<br/> Error Page를 보여준다.
<br/>(error.js파일은 해당 page.tsx 파일에만 적용)

## 4.0 Vercel에 배포

Next.js는 Vercel을 통해 배포할 수 있다.
<br/>github와 연동하여 github에 업데이트를 할때마다 빌드가 새로 되어서 최신화면을 볼 수 있다.

## 4.1 CSS Module

여러 라이브러리를 사용해도 되지만 Next.js는 .module.css 확장자를 사용하는 css모듈을 기본적으로 지원한다.
<br/> 방법은 javascript처럼 import를 해야한다.
<br/> ex) import style from '../styles/navigation.module.css;
<br/> ex) nav className={styles.nav}
<br/> 예제처럼 사용을 해야한다.

<br/> Global Styles
<br/> 글로벌 스타일은 앱 디렉터리 내의 모든 레이아웃, 페이지 또는 컴포넌트를 가져올 수 있음.

## 4.5 Deployment

prefetch => Link 컴포넌트가 사용자의 뷰포트에 들어갈 때 발생
<br/>백그라운드에서 prefetch 및 load하여 클라이언트 측 성능 향상
<br/>prefetch는 프로덕션에서만 활성화됩니다.
