---
layout: post
title:  "[React] 시작하기"
date:   2019-05-16 16:04 :07
categories: react
tags: react
image: 
---

# React

## CodePen.io 사용
- JavaScript Preprocessor에 Babel 선택
    - ES6문법을 그 이전 문법으로 바꾸어줌
    - 구 버전 웹사이트에 적용시키기 위해
- Quick-add 에서 React, React-Dom 선택
    - React는 Component 담당
    - React-Dom은 렌더링 부분 담당

## Componet
- 자바스크립트 class를 말한다 
- ReactComponent 라는 클래스를 상속
- 모든 컴포넌트에는 `render()`메소드가 있다.

## Render
- component가 어떻게 생길지 결정한다.
- JSX
    - javascript에서 html형태로 작성할 수 있다.
    - 꼭 container element안에 포함 시켜야 한다.

    ~~~
    /* 에러 발생 코드 */
    render(){
        return(
            <h1>HI</hi>
            <h2>I am Error</h2>
        );
    }
    /* 컴포넌트에서 여러 Element를 렌더링 할 때 꼭 conainer element안에 포함시켜야 한다 */
    render(){
        return(
            <div>
                <h1>HI</hi>
                <h2>I am Error</h2>
            </div>
        );
    }
    ~~~
    - JavaScript 변수를 보여주고 싶을 때는 {}로 wrapping한다.
    ~~~
    render(){
        let text = "Hello React!";
        return(
            <div>{text}</div>
        );
    }
    ~~~
    - 변수 선언시에는 let 사용
    - style 설정시 string 형식을 사용하지 않고 key가 camelCase인 객체를 사용 해야한다.
    ~~~
    render(){
        let style={
            color:'aqua',
            backgroundColor : 'black',
        }
        return(
            <div style={style}>React Codelab</div>
        );
    }
    ~~~
    - 주석은 {/* ~~ */}의 형태여야 한다.
    - 주석은 container element(return)안에 작성되어야한다.


## ReactoDOM
- 실제 페이지에 JSX코드를 렌더링 할 때 사용된다
- 첫번째 인수는 렌더링 할 컴포넌트, 두번째 인수는 이 컴포넌트를 렌더링 할 element(id)

## Props
- 컴포넌트 내부의 Immutable Data
    - 변하지않는 데이터를 사용할 때 
- JSX 내부에 `{this.props.propsName}`
- 컴포넌트를 사용할 때, <> 괄호 안에 `propsName ="value"`
- this.props.children은 기본적으로 갖고있는 props로서, `<Cpnt>`여기에 있는 값이 들어간다.`</Cpnt>`


## props의 기본값 설정하기
- 컴포넌트 선언이 끝난후 `Component.defaultProps= {...}`객체를 설정한다.
~~~
class App extends React.Component{
    render(){
        return(
            <div>{this.props.value}</div>
        );
    }
}

App.defaultProps={
    value:0,
};
~~~
  
- Type 검증
    - 특정 props 값이 특정 타입이 아니거나 필수 props인데 입력을 안한 경우 확인가능
    - `Component.propTypes={...}`
~~~
class App extends React.Component{
    render(){
        return(
            <div>
                {this.props.value}
                {this.props.secondValue}
                {this.props.thirdValue}
            </div>
        );
    }
}

App.propTypes={
    value : React.PropTypes.string,
    seoncdValue : React.PropTypes.number,
    thirdValue : React.PropTypes.any.isRequried,
}
~~~


## State
- 유동적인 데이터
- JSX 내부에 `{this.state.stateName}`
- 초기값 설정이 필수, 생성자(constructor)에서 `this.state={}`으로 설정
- 값을 수정할 때에는 `this.setState({...})`을 사용하여 컴포넌트 내에서 값 수정 
- 렌더링 된 다음엔 `this.state=` 절대 사용하지 말것, 즉 생성자에서 사용하지 못함

~~~
class Counter extends React.Component{
  constructor(props){
    super(props);
    this.state ={
    value:0,  
    }
    // 바인딩을 꼭 해줘야 this가 여기 클래스에서 사용하는 this인지 안다
    this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick(){
    this.setState({

      value: this.state.value+1
    })
    /* 이렇게 하지말기!
    this.state.value = this.state.vlaue+1;
    this.forceUpdate();
    */
  }
  
  render(){
    return(
      <div>
        <h2>{this.state.value}</h2>
        <button onClick={this.handleClick}>Press Me</button>
      </div>
    )
  }
}

class App extends React.Component{
  render(){
    return(
      <Counter/>
    );
   }
};

ReactDOM.render(
  <App></App>, document.getElementById("root"));
  ~~~

## Component Mapping
- 비슷한 코드를 반복해서 업데이트 하는 방법

> ### Map
> - 데이터 렌더링 할 때 사용하는 자바스크립트 함수
> - map()메소드는 파라미터로 전달 된 함수를 통하여 배열 내의 각 요소를 처리해서 그 결과로 새로운 배열을 생성한다.  
> - `arr.map(callback,[thisArg])`
>   - callback : 새로운 배열의 요소를 생성하는 함수로서, 다음 세가지 인수를 가진다
>   - currentValue : 현재 처리되고 있는 요소
>   - index : 현재 처리되고 있는 요소의 index값
>   - array : 메소드가 불려진 배열
>  - thisArg(선택항목) : callback함수 내부에서 사용 할 this 값을 설정
