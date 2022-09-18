---
title: redux 简单实战
Categories: react, redux
---



### 三大概念

#### **state**

- ​	store
- ​    单一 
- ​	唯一 （当前项目唯一）
- ​	适合同构（服务端的store 可以 注入到客户端）。
- ​    撤销/重做
- ​    只读

#### action

​	一个纯粹的js对象字面量 （**{type: 'add', payload: 1}**）

​	用来修改state的行为

​	只能用来修改 **state** ，且 **state** 只能用 **action** 修改

#### reducer

​	载体 

​	[纯函数](https://zh.wikipedia.org/wiki/%E7%BA%AF%E5%87%BD%E6%95%B0)

​	用来修改state的方法



**一个demo**

示例：TODO列表

```jsx
// 伪代码

import {createStore} from "redux";
import reducers from "reducers";
const store = createStore(reducers);
// 如果store 有修改那么这里的订阅会触发
store.subcribe((state) => {
  console.log(state.getState());
})
export store;
reducer
	todoInitState = [];
	const changeTodo = () => {} /* 修改状态并返回一个新的 TODO */ 
	todoReducer(state = todoInitState, action)
  	switch (action.type) {
      case TODO_ADD:
      	return [todoInitState, action.payload];
      case TODO_COMPLETE:
        const findTodo = state.find(action.payload);
        const updateTodo = changeTodo(findTodo);
        const newState = [...state.splice(findTodo.index, 1, updateTodo)]
        return newState;
      case TODO_DELETE:
        ...
        return state;
      default:
        return state;
    }
  filterReducer
  	
export combineReducers({todos: todoReducer, filter: filterReducer})
action
	const TODO_ADD = 'add';
	const TODO_COMPLETE = 'complete'
	const TODO_DELETE = 'delete'
  
  
// 结合react 
// 使用react-redux
// App.jsx
import {Provider} from "react-redux";
import Store from "./store";
function App(props) {
  return <div id="root">
  	<Provider Store="Store">
			{props.children}    
    </Provider>
  </div>
}

// todoListjsx
import store
import ACTION from './action'
import Todo;
function TodoList() {
  const clickAdd = () => {
    store.dispatch({type: ACTION.TODO_ADD, payload: 'text'})
  }
  const changeTodo(todoId) {
    store.dispatch({type: ACTION.TODO_COMPLETE, payload: {id: todoId, state: '1'}})
  };
  const list = store.getStates().todos;
  return (<div>
      <button onClick={clickAdd}>新增</button>
      {list.map( todo => <Todo {...todo} onChange={changeTodo} />}}
  </div>)
}
// todojsx
function Todo(props) {
  return <div>
    <button onClick={props.changeTodo}></button>
  </div>
}



```

```jsx
// connect 版本
+ import {connect} from "react-redux";

onst mapStateToProps = (state) => {
  return { list: state.list };
};
const mapDispatchToProps = (dispatch) => ({});
function App(props) {
-  const selectors = useSelector((state) => state);
+  const selectors = props;
+  const dispatch = props.dispatch;
-  const dispatch = useDispatch();

  const [todoList, setTodoList] = useState(selectors.list.filter((item) => item.status === 0));
  const [ongoingList, setOngoingList] = useState(selectors.list.filter((item) => item.status === 1));
  const [doneList, setDoneList] = useState(selectors.list.filter((item) => item.status === 2));
  const [showAdd, setShowAdd] = useState(false);
  const COLUMN_BG_COLORS = {
    todo: "#C9AF97",
    ongoing: "#FFE799",
    done: "#C0E8BA",
  };
  const handleAdd = (evt) => {
    setShowAdd(true);
  };
  console.log("render");
  const handleSubmit = (title) => {
    dispatch({ type: "ADD_ITEM", payload: { title, status: 0, date: new Date().toDateString() } });
    setShowAdd(false);
  };
  useEffect(() => {
    setTodoList(selectors.list.filter((item) => item.status === 0));
  }, [selectors.list]);
  const changeHandler = (key) => {};
}
export default connect(mapStateToProps)(App);

```



```jsx
// hooks 方式
import { useDispatch, useSelector } from "react-redux"
function TodoList() {
  const dispatch = useDispatch();
  const selector = useSelector();
  const clickAdd = () => {
-    store.dispatch({type: ACTION.TODO_ADD, payload: 'text'})
+    dispatch({type: ACTION.TODO_ADD, payload: 'text'})    
  }
  const changeTodo(todoId) {
    dispatch({type: ACTION.TODO_COMPLETE, payload: {id: todoId, state: '1'}})
  };
-  const list = store.getStates().todos;
+  const list = selector.todos;
  return (<div>
      <button onClick={clickAdd}>新增</button>
      {list.map( todo => <Todo {...todo} onChange={changeTodo} />}}
  </div>)
}

```



#### 概念

Immutable（immutable-js ）

selector（Reselect）