# React-Study
React-Study

## React 설치

>  Node 14.0.0 혹은 상위 버전 및 npm 5.6 혹은 상위 버전이 필요합니다

```ps
npx create-react-app my-app
cd my-app
npm start
```

> 첫 번째 줄의 ‘npx’는 실수가 아니며 npm 5.2+ 버전의 패키지 실행 도구입니다.

# JSX

## JSX란?

React에서는 본질적으로 렌더링 로직이 UI 로직(이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등)과 연결된다는 사실을 받아들입니다.

React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 “컴포넌트”라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리합니다. 

React는 JSX 사용이 필수가 아니지만, 대부분의 사람은 JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각합니다. 또한 React가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해줍니다.

## JSX에 표현식 포함하기

아래 예시에서는 name이라는 변수를 선언한 후 중괄호로 감싸 JSX 안에 사용하였습니다.

```javascript
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

JSX의 중괄호 안에는 유효한 모든 JavaScript 표현식을 넣을 수 있습니다.

아래 예시에서는 JavaScript 함수 호출의 결과인 formatName(user)을 ```<h1>``` 엘리먼트에 포함했습니다.
  
```javascript
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
  
## JSX도 표현식입니다

컴파일이 끝나면, JSX 표현식이 정규 JavaScript 함수 호출이 되고 JavaScript 객체로 인식됩니다.

즉, JSX를 if 구문 및 for loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있습니다.

```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

##	JSX 속성 정의

어트리뷰트에 따옴표를 이용해 문자열 리터럴을 정의할 수 있습니다.

```javascript
const element = <a href="https://www.reactjs.org"> link </a>;
```
	
중괄호를 사용하여 어트리뷰트에 JavaScript 표현식을 삽입할 수도 있습니다.
	
```javascript
const element = <img src={user.avatarUrl}></img>;
```

어트리뷰트에 JavaScript 표현식을 삽입할 때 중괄호 주변에 따옴표를 입력하지 마세요. 따옴표(문자열 값에 사용) 또는 중괄호(표현식에 사용) 중 하나만 사용하고, 동일한 어트리뷰트에 두 가지를 동시에 사용하면 안 됩니다.

>	JSX는 HTML보다는 JavaScript에 가깝기 때문에, React DOM은 HTML 어트리뷰트 이름 대신 camelCase 프로퍼티 명명 규칙을 사용합니다.

예를 들어, JSX에서 class는 className가 되고 tabindex는 tabIndex가 됩니다.

##	JSX로 자식 정의

태그가 비어있다면 XML처럼 /> 를 이용해 바로 닫아주어야 합니다

```javascript
const element = <img src={user.avatarUrl} />;
```

JSX 태그는 자식을 포함할 수 있습니다.

```javascript
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

##	JSX는 주입 공격을 방지합니다

JSX에 사용자 입력을 삽입하는 것은 안전합니다.

```javascript
const title = response.potentiallyMaliciousInput;
// 이것은 안전합니다.
const element = <h1>{title}</h1>;
```

기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 이스케이프 하므로, 애플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않습니다. 모든 항목은 렌더링 되기 전에 문자열로 변환됩니다. 이런 특성으로 인해 XSS (cross-site-scripting) 공격을 방지할 수 있습니다.

##	JSX는 객체를 표현합니다.

Babel은 JSX를 React.createElement() 호출로 컴파일합니다.

다음 두 예시는 동일합니다.

```javascript
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```javascript
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

React.createElement()는 버그가 없는 코드를 작성하는 데 도움이 되도록 몇 가지 검사를 수행하며, 기본적으로 다음과 같은 객체를 생성합니다.

```javascript

// 주의: 다음 구조는 단순화되었습니다
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

이러한 객체를 “React 엘리먼트”라고 하며, 화면에서 보고 싶은 것을 나타내는 표현이라 생각하면 됩니다. React는 이 객체를 읽어서, DOM을 구성하고 최신 상태로 유지하는 데 사용합니다.

#   엘리먼트 렌더링

>   엘리먼트는 React 앱의 가장 작은 단위입니다.

엘리먼트는 화면에 표시할 내용을 기술합니다.

```javascript
const element = <h1>Hello, world</h1>;
```

브라우저 DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체이며(plain object) 쉽게 생성할 수 있습니다. React DOM은 React 엘리먼트와 일치하도록 DOM을 업데이트합니다.

##  DOM에 엘리먼트 렌더링하기

HTML 파일 어딘가에 <div>가 있다고 가정해 봅시다.

```html
<div id="root"></div>
```

이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 “루트(root)” DOM 노드라고 부릅니다.

React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있습니다. React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM 노드가 있을 수 있습니다.

React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 ReactDOM.render()로 전달하면 됩니다.

```javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

##  렌더링 된 엘리먼트 업데이트하기

React 엘리먼트는 불변객체입니다. 엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없습니다. 엘리먼트는 영화에서 하나의 프레임과 같이 특정 시점의 UI를 보여줍니다.

지금까지 소개한 내용을 바탕으로 하면 UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 ReactDOM.render()로 전달하는 것입니다.

예시로 똑딱거리는 시계를 살펴보겠습니다.

```javascript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="js,result" data-slug-hash="gwoJeZ" data-user="gaearon" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/gaearon/pen/gwoJeZ">
  Hello World in React</a> by Dan Abramov (<a href="https://codepen.io/gaearon">@gaearon</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

<iframe height="300" style="width: 100%;" scrolling="no" title="Hello World in React" src="https://codepen.io/gaearon/embed/gwoJeZ?default-tab=js%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/gaearon/pen/gwoJeZ">
  Hello World in React</a> by Dan Abramov (<a href="https://codepen.io/gaearon">@gaearon</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

위 함수는 setInterval() 콜백을 이용해 초마다 ReactDOM.render()를 호출합니다.

>   실제로 대부분의 React 앱은 ReactDOM.render()를 한 번만 호출합니다. 

