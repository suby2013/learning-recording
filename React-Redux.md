# withRouter
* 作用：<br>
 redux 的 connect 方法重写了组件的 shouldComponentUpdate 方法，导致不能响应 location 的变化而重新渲染组件。<br>
 withRouter 写在 connect 外面，withRouter 的 shouldComponentUpdate 不会被重写，组件会成功的重新渲染。<br>
* 用法：<br>
const App = withRouter(connect (mapStateToProps,mapDispatchToProps))(App);<br>
每个子组件可以通过this.props 获取history、location、match三个对象<br>
const {history、location、match} = this.props;<br>

# react-thunk
* 作用：<br>
返回的是一个柯里化过的函数，从而将同步的 action 转为异步的 action。 <br>
redux-thunk使得action变成可以执行异步逻辑的action，将请求放在异步action中，最后还是要调用同步action传入store来更新state。 <br>
* 实现源码：<br>
```
function createThunkMiddleware(extraArgument) {
  return function({ dispatch, getState }) {
    return function(next){
      return function(action){
        <!--如果action是函数，则调用函数-->
        if (typeof action === 'function') {
          return action(dispatch, getState, extraArgument);
        }
        return next(action);
      };
    }
  }
}
```
# connect
* 作用：<br>
store和组件联系在一起 <br> 
* 用法：<br>
connect方法接受四个参数：常用两个参数 mapStateToProps，mapDispatchToProps，返回处理后的组件<br>
mapStateToProps可以将对应的state作为prop注入对应的子组件，mapDispatchToProps 把指定的action作为props注入对应的子组件<br>
```const VisibleTodoList = connect(
                mapStateToTodoListProps,
                mapDispatchToTodoListProps
            )(TodoList);
```
# provider
* 作用：<br> 
Provider组件作为做上层组件，需要将store作为参数注入组件中，此后在每个子组件中都可以访问到store这个对象<br>
* 用法：<br>
```ReactDOM.render(
     <Provider store={createStore(App)}>
        <App />
     </Provider>,
     document.getElementById('root')
);
```
