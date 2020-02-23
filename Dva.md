### Dva 如何实现数据增删改查
### 简单计数器
```
import React from 'react';
import dva, { connect } from 'dva';

// 1. Initialize
const app = dva();

// 2. Model
app.model({
  namespace: 'count',
  state: 0,
  reducers: {
    add  (count) { return count + 1 },
    minus(count) { return count - 1 },
  },
});

// 3. View
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

// 4. Router
app.router(() => <App />);

// 5. Start
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
  dispatch({
    //  namespace/reduceType
    type: 'products/delete',
    payload: id,
  });
 ```
 
 ### react-redux  connect 
 connect 方法具体的作用是将store和组件联系在一起 <br>
 connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])(Mycomponent)  <br>
 让组件可以访问redux里面的state,dispatch,并绑定在组件的props上。  <br>
 引入vuex里面的部分state to props 可以定义函数  <br>
 ```
 function mapStateToProps(state) {
  //uesr模块的state
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
 类似Vuex中   <br>
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
