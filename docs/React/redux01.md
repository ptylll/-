### redux 简单demo 
#### 安装第三方模块

npm install --save redux

npm install --save react-redux

npm install --save react-router

#### 实例
```
import React, { Component } from 'react';  
import ReactDOM from 'react-dom';  
import { createStore } from 'redux';  
import { Provider, connect } from 'react-redux';  

class App extends Component{
  render(){
    const {text,onChangeText,onButtonClick,onButtonLgClick} = this.props;
    return(
        <div>
            <h1 onClick={onChangeText}>{text}</h1>
            <button onClick={onButtonClick}>clicke me</button>
            <button onClick={onButtonLgClick}>clicke me + 10</button>
        </div>
    )
  }
}

//action
const changeTextAction = {
  type:'CHANGE_TEXT'
}
const buttonClickAction = {
  type:'BUTTON_CLICK'
}
const onButtonLgAction ={
  type:'BUTTON_LGCLICK'
}

//reducer  处理逻辑
const initialState = {
  text:0
}
const reducer = (state = initialState,action) =>{
  switch(action.type){
    case "CHANGE_TEXT":
      return{
          text:state.text == 'Hello' ? 'world' : 'HELLO'   
      }
    case 'BUTTON_CLICK':
        return{
          text:state.text + 1
        }
    
    case 'BUTTON_LGCLICK':
        return{
          text:state.text + 10
        }    
    default:
        return initialState;
  }
}

//创建store
let store = createStore(reducer);

//映射Redux state到组件的属性  
function mapStateToProps(state){
  return {text:state.text}
}

//映射Redux actions到组件的属性  
function mapDispatchToProps(dispatch){
  return{
    onButtonClick:() =>dispatch(buttonClickAction),
    onChangeText:() =>dispatch(changeTextAction),
    onButtonLgClick:() =>dispatch(onButtonLgAction),
  }
}

//连接组件  
App = connect(mapStateToProps, mapDispatchToProps)(App)  

//渲染组件  
ReactDOM.render(
  <Provider store={store}>
      <App />
  </Provider>
  ,document.getElementById('root')
)
```