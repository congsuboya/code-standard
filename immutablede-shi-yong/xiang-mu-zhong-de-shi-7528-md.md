## <a name="types">包裹State</a>

 - 模块的state要保证是immutable类型的。调用fromJS();
    
 
    ```javascript
    
       //moduleName/reducers/reducers
       import * as types from '../actions/actionType';
       import config from '../config'
       import { fromJS } from 'immutable';
        
       const initState = fromJS(config);//进行包裹
        
       function reduxReducers(state = initState, action) {
            switch (action.type) {
                case types.XSY_REDUX_DEMO_INIT_STATE:
                    return state.update('instances', v => v.set(action.Id, v.get('default')));
                case types.XSY_REDUX_DEMO_CLICK:
                    return state.updateIn(['instances', action.Id, 'num'], v => (v + 1));
                default:
                    return state;
            }
        }
       
    ```


## <a name="types">类中的使用</a>

- 因为redux的state是immutable类型，调用和取值就与以前有区别

    ```javascript
render(){
    //good
    let data = this.props.state.getIn(['instances',this.props.componentID,'data']);
            
    //bad
    let { data } = this.props.state.instances[this.props.componetID];//会报错
    ...
    }

    ```

- 用在shouldComponentUpdate(nextProps, nextState)中优化render次数

```javascript
    shouldComponentUpdate(nextProps, nextState){
        if (this.props.state.getIn(['instances', this.props.componentID]) === nextProps.state.getIn(['instances', this.props.componentID])) {
          return false
        }
        return true;
    }
    
    ```


- 当改变一个对象下面一个List的没个item中一个属性的值

```javascript

    //initState = {
        'instances':{
            '23123':{
                name:'demo',
                value:[
                    {click:true,id,1},
                    {click:true,id,2},
                    {click:true,id,3},
                    {click:true,id,4},
                    {click:true,id,5},
                    {click:true,id,6},
                    ....
                    ],
                    ....
                    },
            'defaule':{
                    ...
                }
            }
     }
    
   //把上面initState下面的 23123这个对象下面的value的每个Item的click置为非。并插入showId字段
   function reduxReducers(state = initState, action) {
        switch (action.type) {
             ...
            case types.XSY_REDUX_DEMO_CLICK:
                return state.withMutations(item =>
                    item.updateIn(['instances',action.Id,'values', v => v.map((innerItem,innerIndex) => innerItem.set('showId', innerIndex)))
                        .setIn(['instances',action.Id,'values', v =>  v.map((innerItem,innerIndex) => innerItem.update('showId',v=>!v ))))
                     ...    
            default:
                return state;
        }
    }
    
    ```

- 因为现阶段列表不支持immutable类型的数据列表，传入原生层面时也是无法解析的。所以在这两个地方用到时需要用到toJS()方法。

```javascript
    render(){
        let data = this.props.state.getIn(['instances',this.props.componentID,'data']);
        
        return(
            <FlatList
                ...
                data ={data.toJS()}
                ...
            />)
    }
    
    
    import { NativeModules }  from 'react-native';
    const XSYCustomEntityModule = NativeModules.XSYCustomEntityModule;
    
    toNativePage(){
        let data = this.props.state.getIn(['instances',this.props.componentID,'data']);
        XSYCustomEntityModule.pushWithData(data.toJS())
    }
```


