# study-react

### React
React는 페이스북 UI 라이브러리입니다. 
Component(사용자 정의 태그)를 사용하여 가독성, 재사용성, 유지보수의 엄청난 장점을 가지고 있습니다.   

### 개발환경
1. node.js 설치 npm 설치
2. npm install -g create-react-app 입력하여 설치
3. 작업 폴더로 이동하여 create-react-app . 입력하여 설치
4. 터미널창을 열어 npm run start 로 React 실행
5. ctrl + c 로 종료

### 간단한 리액트 수정
index.js 파일을 열어보면 아래와 같이 작성해 App 컴포넌트를 index.js 에서 연결하여 사용하는 것을 확인 할 수 있습니다. './App'은 뒤에 .js 가 생략된 것이고 App.js 파일을 수정하게 되면 App.js를 사용하고 있는 index 에서도 수정 된 내용이 반영됩니다.
```
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

### 배포
create-react-app은 개발환경에 도움이 되는 여러가지 기능들이 추가 되어 아무런 기능이 없는 페이지라도 용량을 차지하고 있습니다.
이러한 용량을 줄이는 방법으로 터미널에서 npm run build 를 입력하여 build 라는 디렉토리를 생성해 줍니다.
build는 내가 만들어 놓은 파일들을 최적화하여 용량을 줄여 줍니다. 최적화 된 build 디렉토리를 실행 하는 방법은
npx serve -s build 를 통해 실행 할 수 있습니다. 여기서 npx 가 npm 과 다른 점은 npx는 실행 할 때 패키지를 설치하고 실행이 종료되면 패키지를 다시 지워줍니다.