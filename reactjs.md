React Cheat List
===

[![NPM version](https://img.shields.io/npm/v/react.svg?style=flat)](https://npmjs.org/package/react)
[![Downloads](https://img.shields.io/npm/dm/react.svg?style=flat)](https://www.npmjs.com/package/react)
[![Repo Dependents](https://badgen.net/github/dependents-repo/facebook/react)](https://github.com/facebook/react/network/dependents)
[![Github repo](https://badgen.net/badge/icon/Github?icon=github&label)](https://github.com/facebook/react)

A comprehensive React cheat list for beginners
<!--rehype:style=padding-top: 12px;-->

getting Started
----

### introduce

React is a JavaScript library for building user interfaces

- [React official documentation](https://reactjs.org/) _(reactjs.org)_
- [Styled Components Cheat List](./styled-components.md) _(jaywcjlove.github.io)_
- [TypeScript JSX Cheat Sheet](./typescript.md#jsx) _(jaywcjlove.github.io)_

```js
import {createRoot} from 'react-dom/client'
import App from './App'
```

-----

```jsx
const elm = document.getElementById('app')
const root = createRoot(elm);
root.render(<App />);
```

#### Quickly create **React** projects ([CRA](https://github.com/facebook/create-react-app))

```shell
npx create-react-app my-app
```

### Import multiple exports

```jsx
import React, {Component} from 'react'
import ReactDOM from 'react-dom'
```

-----

```jsx
export class Hello extends Component {
  ...
}
export default function World() {
  /* ... */
}
```

Use `export` to export **`Hello`**, `export default` to export **`World`** component

```jsx
import World, { Hello } from './hello.js';
```

Use `import` to import the `Hello` component, used in the example.

### CSS in React components

```jsx {2,5}
import React from "react";
import "./Student.css";

export const Student = (
  <div className="Student"></div>
);
```

NOTE: Class attribute `className`

```jsx
const divStyle = {
  backgroundImage: 'url(' + imgUrl + ')',
};
export const Student = (
  <div style={divStyle}></div>
);
```

### Attributes

```jsx
<Student name="Julie" age={23}
  pro={true} />
```

Access properties in function component `Student`

```jsx
function Student(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Access properties in Class component `Student`

```jsx
class Student extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}
```

`class` components use `this.props` to access the properties passed to the component.

### Children
<!--rehype:wrap-class=row-span-2-->

```jsx
function Example() {
  return (
    <AlertBox>
      <h1>You have pending notifications</h1>
    </AlertBox>
  )
}
```

Function `AlertBox` component

```jsx {4}
function AlertBox(props) {
  return (
    <div className="alert-box">
      {props.children}
    </div>
  );
}
```

-----

```jsx
{props.children}
```

Class `AlertBox` component, the same as the function component `AlertBox` component

```jsx {5}
class AlertBox extends React.Component {
  render () {
    return (
      <div className="alert-box">
        {this.props.children}
      </div>
    );
  }
}
```

-----

```jsx
{this.props.children}
```

`children` is passed as a property of the child component.

### State
<!--rehype:wrap-class=row-span-3-->

State and Hook in functions are new features of React 16.8

```jsx {4,8}
import { useState } from 'react';

function Student() {
  const [count, setCount] = useState(0);
  const click = () => setCount(count + 1);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={click}>
        click me
      </button>
    </div>
  );
}
```

Use `setState` to update the state. The following is the function component to read the state.

```jsx
<p>You clicked {count} times</p>
```

#### State in Class

```jsx {6,12,20}
import React from 'react';

class Student extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 1};
    // Make sure the function can access component properties (ES2015)
    this.click = this.click.bind(this);
  }
  click() {
    const count = this.state.count;
    this.setState({ count: count + 1})
  }
  render() {
    return (
      <div>
        <button onClick={this.click}>
          click me
        </button>
        <p>You clicked {this.state.count} times</p>
      </div>
    );
  }
}
```

Use `setState` to update the state. <yel>~~hooks~~</yel> cannot be used in `class` components. The following is the `class` component reading status

```jsx
<p>You clicked {this.state.count} times</p>
```

### Loop

```jsx
const elm = ['one', 'two', 'three'];
function Student() {
  return (
    <ul>
      {elm.map((value, index) => (
        <li key={index}>{value}</li>
      ))}
    </ul>
  );
}
```

`key` value must be unique among sibling nodes

### Event monitoring

```jsx
export default function Hello() {
  function handleClick(event) {
    event.preventDefault();
    alert("Hello World");
  }

  return (
    <a href="/" onClick={handleClick}>
      Say Hi
    </a>
  );
}
```

### Function injection

```jsx
function addNumbers(x1, x2) {
  return x1 + x2;
}

const element = (
  <div>
    {addNumbers(2, 5)}
  </div>
);
```

### Nesting

```jsx
import { useState } from 'react'
import Avatar from './Avatar';
import Profile from './Profile';

function Student() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <Avatar src={count} />
      <Profile username={count} />
    </div>
  );
}
```

### Portals

React does not create a new div. It just renders the child elements into `domNode`. `domNode` is a valid DOM node that can be anywhere.

```jsx
render() {
  return ReactDOM.createPortal(
    this.props.children,
    domNode
  );
}
```

Provides an excellent solution for rendering child nodes to DOM nodes that exist outside the parent component.

### Fragment
<!--rehype:wrap-class=row-span-2-->

```jsx {1,6,9}
import { Fragment } from 'react'
import Avatar from './Avatar';
import Profile from './Profile';

const Student = () => (
  <Fragment>
    <Avatar src="./demo.jpg" />
    <Profile username="name" />
  </Fragment>
);
```

Starting with `v16.2.0` `Fragment` can be used to return multiple child nodes without adding additional wrapper nodes to the DOM. Or use `<></>`, the effect is the same.

```jsx {2,5}
const Student = () => (
  <>
    <Avatar src="./demo.jpg" />
    <Profile username="name" />
  </>
);
```

查看: [Fragments & strings](https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-render-return-types-fragments-and-strings)

### Return string

```jsx {2}
render() {
  return 'Look ma, no spans!';
}
```

You can just return a string. Check out: [Fragments & strings](https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-render-return-types-fragments-and-strings)

### Return array

```jsx
const Student = () => [
  <li key="A">First item</li>,
  <li key="B">Second item</li>
];
```

Don't forget `key`! Check out: [Fragments & strings](https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-render-return-types-fragments-and-strings)

### Refs Forward

```jsx
const FancyButton = React.forwardRef(
  (props, ref) => (
    <button ref={ref} className="btn">
      {props.children}
    </button>
  )
);
```

#### use

```jsx
// You can directly get the ref of the DOM button:
const ref = React.createRef();

<FancyButton ref={ref}>
  click me
</FancyButton>;
```

### The ref attribute is used internally in the Class component

```jsx {6,10}
import {Component,createRef} from 'react'

class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.myRef = createRef();
  }

  render() {
    return <div ref={this.myRef} />;
  }
}
```

Tip: Refs work with class components, but not with function components (unless you use useRef hook, see [hooks](#hooks))

### The ref attribute is used internally in function components

```jsx {3,9}
function CustomTextInput(props) {
  //$input must be declared here so that ref can refer to it
  const $input = useRef(null);
  function handleClick() {
    $input.current.focus();
  }
  return (
    <div>
      <input type="text" ref={$input} />
      <input
        type="button" value="Focus on text input"
        onClick={handleClick}
      />
    </div>
  );
}
```

### Strict Mode StrictMode

```jsx {3,8}
<div>
  <Header />
  <React.StrictMode>
    <div>
      <ComponentOne />
      <ComponentTwo />
    </div>
  </React.StrictMode>
  <Footer />
</div>
```

-----

- [Identifying unsafe lifecycles](https://zh-hans.reactjs.org/docs/strict-mode.html#identifying-unsafe-lifecycles)
- [Warning about legacy string ref API](https://zh-hans.reactjs.org/docs/strict-mode.html#warning-about-legacy-string-ref-api-usage)
- [Warning about using the deprecated findDOMNode method](https://zh-hans.reactjs.org/docs/strict-mode.html#warning-about-deprecated-finddomnode-usage)
- [Detecting unexpected side effects](https://zh-hans.reactjs.org/docs/strict-mode.html#detecting-unexpected-side-effects)
- [Detecting outdated context API](https://zh-hans.reactjs.org/docs/strict-mode.html#detecting-legacy-context-api)
- [Ensuring reusable state](https://zh-hans.reactjs.org/docs/strict-mode.html#ensuring-reusable-state)

Tools that highlight potential issues in your application. Please see: [strict mode](https://zh-hans.reactjs.org/docs/strict-mode.html)

### Profiler
<!--rehype:wrap-class=col-span-2-->

Measuring how often a React application renders and how much it costs

```jsx
<Profiler id="Navigation" onRender={callback}>
  <Navigation {...props} />
</Profiler>
```

To analyze the `Navigation` component and its children. It should be used only when needed.

:- | :-
:- | :-
`id(string)` | The `id` of the `Profiler` tree where the submission occurred
`onRender(function)` | This function is called when any component in the component tree "submits" an update

#### onRender callback function

:- | :-
:- | :-
`phase: "mount" \| "update"` | Determine whether the re-rendering is caused by changes in `props`/`state`/`hooks` or "first load"
`actualDuration: number` | The time spent rendering the Profiler and its children for this update
`baseDuration: number` | The duration of the most recent render of each component in the Profiler tree
`startTime: number` | The timestamp when React started rendering in this update
`commitTime: number` | The timestamp at the end of the React commit phase in this update
`interactions: Set` | A set of "[interactions](https://fb.me/react-interaction-tracing)" that will be tracked when updates are made

default value
---

### Class component default props
<!--rehype:wrap-class=row-span-2-->

```jsx
class CustomButton extends React.Component {
  // ...
}
CustomButton.defaultProps = {
  color: 'blue'
};
```

#### use

```jsx
<CustomButton /> ;
```

If no value is passed `props.color` will be automatically set to `blue`

### Class component default state
<!--rehype:wrap-class=row-span-2-->

```jsx
class Hello extends Component {
  constructor (props) {
    super(props)
    this.state = { visible: true }
  }
}
```

Set the default state in constructor()`.

```jsx
class Hello extends Component {
  state = { visible: true }
}
```

### Function component default props

```jsx
function CustomButton(props) {
  const { color = 'blue' } = props;
  return <div>{color}</div>
}
```

### Function component default state

```jsx
function CustomButton() {
  const [color, setColor]=useState('blue')
  return <div>{color}</div>
}
```

JSX
---

### introduce
<!--rehype:wrap-class=row-span-2-->

`JSX` is just syntactic sugar for the `React.createElement(component, props, ...children)` function

```jsx
<MyButton color="blue" shadowSize={2}>
  click me
</MyButton>
```

will compile to

```js
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'click me'
);
```

no child node

```jsx
<div className="sidebar" />
```

will compile to

```js
React.createElement(
  'div',
  {className: 'sidebar'}
)
```

### JSX dot syntax

```jsx
const Menu = ({ children }) => (
  <div className="menu">{children}<div>
);

Menu.Item = ({ children }) => (
  <div>{children}<div>
);

<Menu>
  <Menu.Item>Menu 1</Menu.Item>
  <Menu.Item>Menu 2</Menu.Item>
<Menu>
```

### JSX Element

```jsx
let element = <h1>Hello, world!</h1>;
let emptyHeading = <h1 />;

const root = ReactDOM.createRoot(
  document.getElementById('root')
);

const element = <h1>Hello, world</h1>;
root.render(element);
```

Reference: [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)

### JSX Properties

```jsx
const avatarUrl = "img/picture.jpg"
const element = <img src={avatarUrl} />;

const element = (
  <button className="btn">
    click me
  </button>
);
```

NOTE: Class attribute `className`

### JSX expression

```jsx
let name = 'Zhang San';
let element = <h1>Hello, {name}</h1>;

function fullName(firstName, lastName) {
  return firstName + ' ' + lastName;
}
let element = (
  <h1>
    Hello, {fullName('三', '张')}
  </h1>
);
```

### JSX style

```jsx
const divStyle = {
  color: 'blue',
  backgroundImage: 'url(' + imgUrl + ')',
};
function MyComponent() {
  return <div style={divStyle}>Component</div>;
}
```

### JSX dangerouslySetInnerHTML

```jsx
const markup = {__html: 'I· you' };

const MyComponent = () => (
  <div dangerouslySetInnerHTML={markup} />
);
```

`dangerouslySetInnerHTML` is React's replacement for `innerHTML` for the browser DOM.

### JSX htmlFor

```jsx
const MyComponent = () => (
  <div>
    <input type="radio" id="ab" name="v">
    <label for="ab">HTML</label>
  </div>
);
```

`for` is a reserved word in `JS`, JSX elements use `htmlFor` instead

### JSX defaultValue

Attributes of uncontrolled components, set the `value` when the component is mounted for the first time

```jsx
<textarea defaultValue="Hello" />
```

`<input>`, `<select>` and `<textarea>` support value attribute

### JSX defaultChecked

Properties of uncontrolled components, set whether the component is selected

```jsx
<input type="radio" defaultChecked />
```

When the type is `checkbox` or `radio`, the component supports the checked attribute

### JSX className

Attribute is used to specify the `class` of `CSS`

```jsx
<div className="warp">...</div>
```

When using [Web Components](https://developer.mozilla.org/zh-CN/docs/Web/Web_Components) in React, use the `class` attribute instead

### JSX conditional rendering
<!--rehype:wrap-class=row-span-2-->

```jsx
import React from "react";

function formatName(user) {
  return user.firstName 
    + ' ' 
    + user.lastName;
}

export function Greeting(user) {
  if (user) {
    return (
      <h1>Hello, {formatName(user)}!</h1>
    );
  }
  return (
    <h1>Hello, sir. </h1>
  );
}
```

Note: Components must always return something.

#### use

```jsx
<Greeting firstName="三" lastName="张" />
```

### JSX ternary operator/and operator&&

```jsx
export default function Weather(props) {
  const isLoggedIn = props.isLoggedIn;
  return (
    <div>
      <b>{isLoggedIn ? 'Has' : 'Not'}</b>Logged in.
    </div>
  );
}
```

-----

```js
{isShow && <div>内容</div>}
```

### JSX Component

```jsx
<Dropdown>
  drop-down list
  <Menu>
    <Menu.Item>Menu 1</Menu.Item>
    <Menu.Item>Menu 2</Menu.Item>
    <Menu.Item>Menu three</Menu.Item>
  </Menu>
</Dropdown>
```

Component names are named in camelCase.

### JSX element variables

```jsx
function Greeting(props) {
  let button;
  if (props.isLoggedIn) {
    button = <UserGreeting />;
  } else {
    button = <GuestGreeting />;
  }
  return <div>{button}</div>;
}
```

### JSX comments

```jsx
function Student() {
  const [count, setCount] = useState(0);
  return (
    <Fragment>
      {/*Write comments here*/}
    </Fragment>
  );
}
```

components
----

### Function component
<!--rehype:wrap-class=row-span-2-->

```jsx
import React from 'react';

const UserName = () => <h1>Kenny</h1>;

export default function UserProfile() {
  return (
    <div className="UserProfile">
      <div>Hello</div>  
      <UserName />
    </div>
  );
}
```

NOTE: Every component requires a root element, [more instructions](https://reactjs.org/docs/components-and-props.html).

### Class component

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>{this.props.name}</h1>;
  }
}
```

### Class component API
<!--rehype:wrap-class=row-span-2-->

#### Additional API

:- | -
:- | -
`this.forceUpdate()` | Force re-rendering
`this.setState({ ... })` | Update status
`this.setState(state =>{ ... })` | Update state

#### Attributes

:- | -
:- | -
`defaultProps` | default props
`displayName` | Display component name (for debugging)

#### Instance properties

:- | -
:- | -
`this.props` | Component accepts parameters
`this.state` | In-component state

### Pure components

```jsx
import React, {PureComponent} from 'react'

class MessageBox extends PureComponent {
  ···
}
```

### High-order components

```jsx
import React, { Component } from 'react';
//Higher-order componentswith
const with = data => WrappedComponent => {
  return class extends Component {
    constructor(props) {
      super(props);
    }
    render() {
      return (
        <WrappedComponent data={data} />
      )
    }
  }
}
```

Use higher-order components

```jsx
const LowComponent = (props) => (
  <div>{props.data}</div>
);

const MyComp = with('Hello')(LowComponent)
```

### Inclusion relationship

```jsx
function FancyBorder(props) {
  return (
    <div className={'Fancy'+props.color}>
      {props.children}
    </div>
  );
}
```

Components can be nested via JSX

```jsx
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="title">Welcome</h1>
      <p className="message">
        Thank you for visiting our spaceship
      </p>
    </FancyBorder>
  );
}
```

### Passed as parameters

```jsx
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="left">
        {props.left}
      </div>
      <div className="right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={<Contacts />}
      right={<Chat />}
    />
  );
}
```

Pass the two component parameters `left` and `right` to the component `SplitPane`

### Embed internal components

```jsx {2}
import React from 'react';
import UserAvatar from "./UserAvatar";

export default function UserProfile() {
  return (
    <div className="UserProfile">
      <UserAvatar />
      <UserAvatar />
    </div>
  );
}
```

NOTE: Assume `UserAvatar` is declared in `UserAvatar.js`

### Embed external components

```jsx {2}
import React from 'react';
import {Button} from 'uiw';
export default function UserProfile() {
  return (
    <div className="UserProfile">
      <Button type="primary">
        main button
      </Button>
    </div>
  );
}
```

Note: The [uiw](http://npmjs.com/uiw) component is found on [npmjs.com](https://www.npmjs.com) and needs to be installed and imported first.

### Dot component syntax tips

```jsx
const Menu = ({ children }) => (
  <div className="menu">{children}<div>
);

Menu.Item = ({ children }) => (
  <div>{children}<div>
);
```

-----

```jsx
<Menu>
  <Menu.Item>Menu 1</Menu.Item>
  <Menu.Item>Menu 2</Menu.Item>
<Menu>
```

Hooks
---

### Hooks API Reference
<!--rehype:wrap-class=row-span-2-->

#### Basic Hook

Method | Description
:- | -
`useState` | Returns a `state`, a function that updates `state`[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usestate)
`useEffect` | Functions that may have side effect code[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#useeffect)
`useContext` | Receives and returns the current value of the `context`[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usecontext)

#### Additional Hooks

Method | Description
:- | -
`useReducer` | Alternative to `useState`[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usestate)
`useCallback` | Returns a callback function[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usecallback)
`useMemo` | Returns a [memoized](https://en.wikipedia.org/wiki/Memoization) value[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usememo )
`useRef` | Returns a mutable `ref` object[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#useref)
`useImperativeHandle` | Instance value exposed to parent component[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#useimperativehandle)
`useLayoutEffect` | Synchronously calling function after DOM changes[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#uselayouteffect)
`useDebugValue` | Display label in developer tools [#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usedebugvalue)
`useDeferredValue` | Accepts and returns a new copy of the value[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usedeferredvalue)
`useTransition` | Waiting state of transition tasks[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usetransition)
`useId` | Used to generate unique ID [#](https://zh-hans.reactjs.org/docs/hooks-reference.html#useid)

#### Library Hooks

Method | Description
:- | -
`useSyncExternalStore` | Read and subscribe to external data sources[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usesyncexternalstore)
`useInsertionEffect` | Triggered synchronously before DOM mutation[#](https://zh-hans.reactjs.org/docs/hooks-reference.html#usesyncexternalstore)

### Functional update
<!--rehype:wrap-class=col-span-2-->

```jsx
function Counter({ initialCount }) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count} <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
    </>
  );
}
```

### useRef

```jsx
function TextInputWithFocusButton() {
  const $input = useRef(null);
  const onButtonClick = () => {
    $input.current.focus();
  };
  return (
    <>
      <input ref={$input} type="text" />
      <button onClick={onButtonClick}>
        focus input
      </button>
    </>
  );
}
```

`current` points to a text input element mounted on the DOM

### useImperativeHandle

```jsx
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} />;
}
FancyInput = forwardRef(FancyInput);
```

Parent component uses

```jsx
<FancyInput ref={inputRef} />
inputRef.current.focus()
```

### useEffect

```jsx
useEffect(() => {
  const subs = props.source.subscribe();
  return () => {
    subs.unsubscribe();
  };
}, [props.source]);
```

### useCallback

```jsx
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

### useMemo

```jsx
const memoizedValue = useMemo(
  () => {
    return computeExpensiveValue(a, b)
  },
  [a, b]
);
```

### useId

```jsx
function Checkbox() {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>
        Do you like React?
      </label>
      <input id={id} type="checkbox" />
    </>
  );
};
```

Used to generate a unique `ID` that is stable across servers and clients while avoiding `hydration` mismatches

### useDebugValue

```jsx
function useFriendStatus(friendID) {
  const [
    isOnline, setIsOnline
  ] = useState(null);
  // ...
  // Display a label next to this Hook in developer tools
  // e.g. "FriendStatus: Online"
  useDebugValue(
    isOnline ? 'Online' : 'Offline'
  );
  return isOnline;
}
```
<!--rehype:className=wrap-text -->

It is not recommended that you add a `debug` value to every custom `Hook`

### componentDidMount & componentWillUnmount

```jsx
useEffect(
  () => {
    // componentDidMount
    // When the component is mounted, you can complete your tasks here
    return () => {
      // componentWillUnmount
      // Execute when uninstalling, clear the effect
    };
  },
  [ ]
);
```

This is a writing method similar to the two life cycle functions of `componentDidMount` & `componentWillUnmount` in the `class` component.

life cycle
---
<!--rehype:body-class=cols-2-->

### Mount
<!--rehype:wrap-class=row-span-2-->

Method | Description
:- | -
`constructor` _(props)_  | 渲染前 [#](https://zh-hans.reactjs.org/docs/react-component.html#constructor)
`static getDerivedStateFromProps()` | Called before calling the `render` method [#](https://zh-hans.reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
`render()` | `class` The only method that must be implemented in the component[#](https://reactjs.org/docs/react-component.html#render)
`componentDidMount()` | Called immediately after the component is mounted (inserted into the DOM tree) [#](https://reactjs.org/docs/react-component.html#componentdidmount)
`UNSAFE_componentWillMount()` | Called before mounting, it is recommended to use `constructor()` [#](https://zh-hans.reactjs.org/docs/react-component.html#unsafe_componentwillmount)

Set initial state on `constructor()`. Add DOM event handlers, timers (etc.) on `componentDidMount()` and then remove them on `componentWillUnmount()`.

### uninstall

Method | Description
:- | -
`componentWillUnmount()` | Called directly before the component is unloaded and destroyed [#](https://zh-hans.reactjs.org/docs/react-component.html#componentwillunmount)

### Obsolete API

Obsolete method | New method
:- | -
~~`componentWillMount()`~~ | `UNSAFE_componentWillMount()`  [#](https://zh-hans.reactjs.org/docs/react-component.html#unsafe_componentwillmount)
~~`componentWillReceiveProps()`~~ | `UNSAFE_componentWillReceiveProps()`  [#](https://zh-hans.reactjs.org/docs/react-component.html#unsafe_componentwillreceiveprops)
~~`componentWillUpdate()`~~ | `UNSAFE_componentWillUpdate()`  [#](https://zh-hans.reactjs.org/docs/react-component.html#unsafe_componentwillupdate)

No longer supported after 17+. After `17` version, only the new `UNSAFE_` lifecycle name can be used.

### renew
<!--rehype:wrap-class=col-span-2-->

Method | Description
:- | -
`static getDerivedStateFromProps(props, state)` | Called before calling `render`, it will be called during initial mounting and subsequent updates [#](https://zh-hans.reactjs.org/docs/react-component. html#static-getderivedstatefromprops)
`shouldComponentUpdate(nextProps, nextState)` | If `false` is returned, `render()` is skipped [#](https://zh-hans.reactjs.org/docs/react-component.html#static-getderivedstatefromprops )
`render()` | Returns the same result every time it is called without modifying the component `state`[#](https://zh-hans.reactjs.org/docs/react-component.html# render)
`getSnapshotBeforeUpdate()` | Capture some information (for example, scroll position) from the DOM before changes occur [#](https://zh-hans.reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)
`componentDidUpdate()` | Use `setState()` here, but remember to compare `props`. This method will not be executed on the first render[#](https://zh-hans.reactjs.org/docs/react-component.html#componentdidupdate)

### Error handling
<!--rehype:wrap-class=col-span-2-->

Method | Description
:- | -
`static getDerivedStateFromError(error)` | Called after the descendant component throws an error, it takes the thrown error as a parameter and returns a value to update `state` [#](https://zh-hans.reactjs.org /docs/react-component.html#static-getderivedstatefromerror)
`componentDidCatch(error, info)` | Called after the descendant component throws an error, it will be called during the "submit" phase, thus allowing side effects to be performed[#](https://zh-hans.reactjs.org/docs/ react-component.html#componentdidcatch)

### render()

```jsx {2}
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### constructor()

```jsx {1}
constructor(props) {
  super(props);
  // Don't call this.setState() here
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

### static getDerivedStateFromError()
<!--rehype:wrap-class=row-span-2-->

```jsx {7,13}
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    //Update state so that the next rendering can clearly degrade the UI
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom downgrade UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

### componentDidUpdate()

```jsx {1}
componentDidUpdate(prevProps) {
  // Typical usage (don't forget to compare props):
  if (this.props.uid !== prevProps.uid) {
    this.fetchData(this.props.uid);
  }
}
```

### getSnapshotBeforeUpdate()

```jsx
getSnapshotBeforeUpdate(prevProps, prevState) {
  // Do we add new items to the list?
  // Capture the scroll position so we can adjust the scroll position later.
  if (prevProps.list.length < this.props.list.length) {
    const list = this.listRef.current;
    return list.scrollHeight - list.scrollTop;
  }
  return null;
}
```

PropTypes property type checking
---

### PropTypes
<!--rehype:wrap-class=row-span-3-->

```jsx
import PropTypes from 'prop-types'
```

-----

:- | -
:- | -
`any` | any type
`(props, propName, component name)=>{}` | Custom validator

#### _Base_

:- | -
:- | -
`string` | string
`number` | array
`func` | function
`bool` | Boolean value
`symbol` | -

#### _Enumeration Enum_

:- | -
:- | -
`oneOf(any)` | enumeration type
`oneOfType([type])` | any one of several types

#### _arrayArray_

:- | -
:- | -
`array` | array
`arrayOf` | An array consists of elements of a certain type

#### _ObjectObject_

:- | -
:- | -
`object` | object
`objectOf` | An object consists of values ​​of a certain type
`instanceOf(...)` | Instance of class
`shape` | Object composed of values ​​of a specific type
`exact` | extra attribute warning

#### _Elements_

:- | -
:- | -
`element` | React element
`elementType` | React element type (i.e. `MyComponent`)
`node` | DOM node

#### _Required_

:- | -
:- | -
`(···).isRequired` | required

See: [Type checking with PropTypes](https://zh-hans.reactjs.org/docs/typechecking-with-proptypes.html)

### basic type

```jsx
MyComponent.propTypes = {
  email:      PropTypes.string,
  seats:      PropTypes.number,
  callback:   PropTypes.func,
  isClosed:   PropTypes.bool,
  any:        PropTypes.any
  symbol:     PropTypes.symbol,
}
```

You can declare properties as JS native types, and they are optional by default.

### Required

```jsx
MyComponent.propTypes = {
  // Ensure that when this prop is not provided, a warning message will be printed
  requiredFunc: PropTypes.func.isRequired,

  // Required data of any type
  requiredAny: PropTypes.any.isRequired,
}
```

You can add `isRequired` after any `PropTypes` property.

### Enumeration

```js
MyComponent.propTypes = {
  // Can only be a specific value, enumeration type.
  optionalEnum: PropTypes.oneOf([
    'News', 'Photos'
  ]),
  // An object can be any of several types
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),
}
```

### Elements

```jsx
MyComponent.propTypes = {
  // Any element that can be rendered
  // (including numbers, strings, elements or arrays)
  // (or Fragment) also contains these types.
  node: PropTypes.node,

  // A React element.
  element: PropTypes.element,

  // A React element type (i.e., MyComponent)
  elementType: PropTypes.elementType,
}
```

### Object Object

```jsx
MyComponent.propTypes = {
  // You can specify that an object consists of values ​​of a certain type
  objectOf: PropTypes.objectOf(
    PropTypes.number
  ),
  // You can specify that an object consists of specific type values
  objectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),
  // Object with extra property warning
  objectWithStrictShape: PropTypes.exact({
    name: PropTypes.string,
    quantity: PropTypes.number
  }),
}
```

### Custom validator

```jsx
MyComponent.propTypes = {
  custom: (props, propName, compName) => {
    if (!/matchm/.test(props[propName])) {
      // It should return an Error object when validation fails
      return new Error(
        'Invalid prop `'
        ` \`${propName}\` provided to ` +
        ` \`${compName}\`. verification failed. `
      );

    }
  },
}
```

Please do not use `console.warn` or throw exceptions as this will not work in `oneOfType`.

### Custom `arrayOf` or `objectOf` validator
<!--rehype:wrap-class=col-span-2 row-span-2-->

```jsx
MyComponent.propTypes = {
  arrayProp: PropTypes.arrayOf((propValue, key, componentName, location, propFullName) => {
    if (!/matchme/.test(propValue[key])) {
      // It should return an Error object when validation fails.
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
}
```

`propValue` is the array or object itself, `key` is their current key.

### Array

```jsx
MyComponent.propTypes = {
  arr: PropTypes.arrayOf(PropTypes.number),
};
```

You can specify that an array consists of elements of a certain type

### Instance of verification class

```jsx
MyComponent.propTypes = {
  message: PropTypes.instanceOf(Message),
};
```

Declare `message` as an instance of the class

See also
----

- [React official Chinese documentation](https://zh-hans.reactjs.org/) _(zh-hans.reactjs.org)_
- [React Lifecycle Methods Diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/) _(projects.wojtekmaj.pl)_
- [React 16 Cheat Sheet](https://reactcheatsheet.com)
- [Awesome React](https://github.com/enaqx/awesome-react) _(github.com)_
