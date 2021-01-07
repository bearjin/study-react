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

### 컴포넌트 만들기
```
class Subject extends Component {
  render() {
    return (
      <header>
        <h1>WEB</h1>
        world wide web!
      </header>
    );
  }
}

class App extends Component {
  render() {
    return (
    <div className="App">
      <Subject></Subject>
      <TOC></TOC>
      <Content></Content>
    </div>
    );
  }
}
```

### props
컴포넌트를 속성을 통해 효율적으로 리팩토링 할 수 있도록 만들어줍니다.
```
class Subject extends Component {
  render() {
    return (
      <header>
          <h1>{this.props.title}</h1>
          {this.props.sub}
      </header>
    );
  }
}

class App extends Component {
  render() {
    return (
    <div className="App">
      <Subject title="WEB" sub="world wide web!!"></Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC></TOC>
      <Content></Content>
    </div>
    );
  }
}
```

### React Developer Tools
크롬 확장프로그램을 통해 리액트로 만들어진 컴포넌트 정보들을 확인 할 수도 변경을 해볼 수도 있습니다.

### Component 파일로 분리하기
컴포넌트 각각의 파일에 export를 지정하여 다른곳에서 사용가능하도록 만들어줍니다. 불러오는 곳에서 import를 지정하여 원하는 컴포넌트를 가져와 사용 할 수 있습니다. 컴포넌트를 각각의 파일로 분리하여 프로젝트를 관리하는데 유용합니다. 
```
import { Component } from 'react';

class Content extends Component{
    render(){
      return(
        <article>   
          <h2>{this.props.title}</h2>
          {this.props.desc}
        </article>
      );
    }
  }

export default Content;
```
```
import './App.css';
import TOC from './components/TOC';
import Content from './components/Content';
import Subject from './components/Subject';
import { Component } from 'react';
```

### state
props는 외부에서 사용하는데 쓰이는 외부장치라면 state는 내부장치로 외부에서 들어오는 props 값을 받아서 내부적으로 컴포넌트를 구현하는 것을 말합니다. 상위 컴포넌트의 state를 하위 컴포넌트의 props로 사용 가능 합니다.
```
class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      subject : { title : 'WEB', sub: 'World Wide Web!'}
    }
  }
  render() {
    return (
    <div className="App">
      <Subject 
        title={this.state.subject.title} 
        sub={this.state.subject.sub}>
      </Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC></TOC>
      <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
    </div>
    );
  }
}
```
```
class TOC extends Component {
  render (){
      var lists = [];
      var data = this.props.data;
      var i = 0;
      while(i < data.length){
          lists.push(<li key={data[i].id}><a href={"/content/" + data[i].id}>{data[i].title}</a></li>)
          i = i + 1;
      }
    return (
      <nav>
        <ul>
          {lists}
        </ul>
      </nav>
    );
  }
}

class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      subject : { title : 'WEB', sub: 'World Wide Web!'},
      contents: [
        {id:1, title:'HTML', desc: 'HTML is for information'},
        {id:2, title:'CSS', desc: 'CSS is for design'},
        {id:3, title:'JavaScript', desc: 'JavaScript is for interactive'}
      ]
    }
  }
  render() {
    return (
    <div className="App">
      <Subject 
        title={this.state.subject.title} 
        sub={this.state.subject.sub}>
      </Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC data={this.state.contents}></TOC>
      <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
    </div>
    );
  }
}
```

### props, state, render 함수
리액트는 props, state의 값이 변경되면 값을 포함하고 있는 컴포넌트의 render 함수가 실행되고 하위 컴포넌트까지도 포함하여 화면이 다시 그려집니다.

### React 이벤트
리액트에서 이벤트 호출은 onClick={function(){}}을 통해 호출 할 수 있습니다. onClick를 통해 함수를 호출 하였을 때 this는 컴포넌트 본인이 아닌 다른 this를 가져 state를 찾지 못합니다(이벤트핸들러 어트리뷰의 값으로 지정한 함수는 이벤트핸들러에 의해 일반함수로 호출되고 this는 전역객체인 window를 가리키게 됩니다. 다만 'strict mode'가 적용된 일반함수 내부의 this는 window가 아닌 undefined가 바인딩 됩니다. class의 내부는 암묵적으로 strict mode가 적용되기 때문에 this는 undefinde가 되는 것 입니다.). 그래서 bind()함수를 통해 this를 컴포넌트 본인으로 지정해 줍니다. constructor에서가 아닌 다른곳에서 state를 변경하기 위해서는 setState({})를 통해 state를 변경할 수 있습니다.
```
<header>
  <h1><a href="/" onClick={function(e){
    e.preventDefault();
    // this.state.mode = 'welcome';
    this.setState({
      mode: 'welcome'
    })
  }.bind(this)}>{this.state.subject.title}</a></h1>
  {this.state.subject.sub}
</header>
```

### 컴포넌트 이벤트 만들기
내가 만든 컴포넌트에 새로운 이벤트를 만들어 사용할 수 있습니다. 
```
<Subject 
  title={this.state.subject.title} 
  sub={this.state.subject.sub}
  onChangePage={function () {
    this.setState({ mode : 'welcome'});  
  }.bind(this)}
  >
</Subject>

class Subject extends Component {
  render() {
    return (
      <header>
          <h1><a href="/" onClick={function (e) {
            e.preventDefault();
            this.props.onChangePage();
          }.bind(this)}>{this.props.title}</a></h1>
          {this.props.sub}
      </header>
    );
  }
}
```
```
<TOC 
  onChangePage={function(id){
    this.setState({mode : 'read', selected_content_id: Number(id)})
  }.bind(this)} 
data={this.state.contents}></TOC>

class TOC extends Component {
  render (){
      var lists = [];
      var data = this.props.data;
      var i = 0;
      while(i < data.length){
          lists.push(
            <li key={data[i].id}>
              <a href={"/content/" + data[i].id} data-id={data[i].id} onClick={function(e){
                e.preventDefault();
                this.props.onChangePage(e.target.dataset.id);
              }.bind(this)}>{data[i].title}</a>
            </li>)
          i = i + 1;
      }
    return (
      <nav>
        <ul>
          {lists}
        </ul>
      </nav>
    );
  }
}
```

### CRUD(create, read, update, delete) - create
shouldComponentUpdate 는 render 이전에 실행이 되고 newProps, newState라는 2가지 매개변수를 가집니다. return 값이 false 일 경우 render를 실행하지 않고 true일 경우에만 render를 실행합니다. 새로운 값을 추가 할 때 push는 원본을 바로 수정하지만 concat은 원본을 수정하지 않고 새로운 값이 추가 된 배열 혹은 객체를 리턴해 줍니다. shouldComponentUpdate 와 concat을 이용하여 값이 변했을 때만 render가 실행 되도록 하여 성능을 향상 시킬 수 있습니다.
```
_article = <CreateContent onSubmit={function(_title, _desc){
  this.max_content_id = this.max_content_id + 1;
  // this.state.contents.push(
  //   {id: this.max_content_id, title: _title, desc: _desc}
  // )
  var newContents = this.state.contents.concat(
    {id: this.max_content_id, title: _title, desc: _desc}
  )
  this.setState({
    contents : newContents
  })
}.bind(this)}></CreateContent>
``` 
```
shouldComponentUpdate(newProps, newState) {
  console.log('===> render shouldComponentUpdate', newProps.data, this.props.data);
  if (this.props.data === newProps.data) {
    return false;
  }
  return true;
}
```