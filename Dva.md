```
学习过程:
1.是什么
2.是用来干嘛的
3.怎么使用
4.为什么，怎么来的，有没有更好的方案(深入)
```
### Dva 如何实现数据增删改
### 简单计数器
```
import React from 'react';
import dva, { connect } from 'dva';

1. Initialize
const app = dva();

2. Model
app.model({
  namespace: 'count',
  state: 0,
  reducers: {
    add  (count) { return count + 1 },
    minus(count) { return count - 1 },
  },
});

3. View
const App = connect(({ count }) => ({
  count
}))(function(props) {
  return (
    <div>
      <h2>{ props.count }</h2>
      <button key="add" onClick={() => { props.dispatch({type: 'count/add'})}}>+</button>
      <button key="minus" onClick={() => { props.dispatch({type: 'count/minus'})}}>-</button>
    </div>
  );
});

4. Router
app.router(() => <App />);

5. Start
app.start('#root');
```
### 简单列表删除

1.model <BR>
```
export default {
    namespace: 'products',
    state: [],
    reducers: {
      'delete'(state, { payload: id }) {
        return state.filter(item => item.id !== id);
      },
    },
  };
```
2.action  <BR>  
```
  namespace/reduceType
  dispatch({
    type: 'products/delete',
    payload: id,
  });
 ```
  3.其他
  ```export default {
  命名空间，当前 Model 的名称
  namespace: 'users',
  state: {
    list: [],
  },
  1.reducer 是一个函数，接受 state 和 action，返回老的或新的 state 。(Action 处理器 )即：(state, action) => state
  2.用来处理同步动作,计算出最新的 State
  3.调用方法 
      1.yield put ({ type: 'reducersName' }); <BR>
      2.组件中：  dispatch({    
      namespace/reduceType  
      type: 'products/delete',  
      payload: id,  <BR>
    }); 
  reducers: {
    save(state, { payload: { data: list} }) {
      return { ...state, list};
    },
  },
  1.Action 处理器
  2.用来处理异步动作
  3.调用方法    namespace/effectsType   
    1.yield put ({ type: 'effectsName' });  
    2.组件中：  dispatch({  
      type: 'products/Add',  
      payload: id
    }); 
  effects: {
    * Generator 函数
    *fetch({ payload: { } }, { call, put }) {
      yield call request
      call：用于调用异步逻辑，ajax请求 promise等
      const { data } = yield call(usersService.fetch, { page });
      yiel put reducer data to modify state
      put：用于触发 Action，类似于 dispatch 对应的type为reducers或者effects
      yield put({
        type: 'save',
        payload: {
          data,
        },
      });
      yeild select filter data of state
      用于从 state 里获取数据 可以filter获取 需要的数据
      const list = yield select(state => state.users.list);
      yield put effect
      put 用来触发Effect或者Reducer方法
     yield put({ type: 'create', payload: { list } });
    },
    *create({ payload: values }, { call, put }) {
      yield put({ type: 'reload' });
    }
  },
  1.订阅，用于订阅一个数据源 根据需要 dispatch 相应的 action。
  2.数据源可以是当前的时间、服务器的 websocket 连接、keyboard 输入、geolocation 变化、history 路由变化等等。
  3.格式为 ({ dispatch, history }) => unsubscribe
  subscriptions: {    
    setup({ dispatch, history }) {
      return history.listen(({ pathname, query }) => {
        if (pathname === '/users') {
            dispatch({ type: 'fetch', payload: query });
        }
      });
    },
  },
};
``` 
 ### react-redux  connect 
 connect 方法具体的作用是将store和组件联系在一起 <br>
 connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])(Mycomponent)  <br>
 让组件可以访问redux里面的state,dispatch,并绑定在组件的props上。  <br>
 引入Redux里面的部分state to props 可以定义函数  <br>
 ```
 function mapStateToProps(state) {
  uesr模块的state
  const { list, total, page } = state.users;
  return {
    list,
    total,
    page,
  };
}
connect(mapStateToProps)(Users);
```
connect后就可以用this.props.list 访问到redux-->user-->list  <br>
 类似Vuex中   this.访问 vuex中的state,getters,actions.
 ```
 import { mapGetters, mapState, mapActions } from 'vuex'
     computed: {
        ...mapState({
            count: state => state.count
        }),
         ...mapGetters({
            other: state => state.other
        })
     }
     methods: {
    ...mapActions(['add'])
    }
```
