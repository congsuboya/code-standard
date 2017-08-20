## container文件夹说明
> 此文件夹内有两个类一个是app.js,一个是containers.js

- ####app类说明

  app类是模块的真正入口。当开发一个模块时，为了方便各个模块单独开发，互相不依赖，此类必须存在，主要是创建单个模块的store和reducer。此类复制过来后基本不需要进行修改。只有需要修改模块需要的传入参数即可。
  同时，为了模块开发完成后方便快速嵌入app的整体框架中，开发模块所需要外界框架传入的参数都在此模块中进行定义，比传参数如下：
  
  ```javascript
  App.defaultProps = {
    componentID: '8148708_2_100222154',
    componentName:{'xsyCustomizeRefer'},
    componentInitUrl: '/json/crm_account_detail/load-compdata.action',
    componentInitParame: {
        query: { "8604058": {} },
        config: { "8604058": { "uuid": "8604058", "widgetType": "xsyCustomizeRefer",           "referItemId": 100267405, "attributes": { "maxGridRowCount": 10, "expandedFlg": 1, 
        "showMode": "card"}, "parentEntityId": 1, "componentId": 2, "childEntityId": 100019307, "_oldid": "100267405", "pid": "8183208", "_inited": true } },
        belongId: 1,
        layoutId: 100222154,
        id: 10827128,
        },
    attributes:{ "maxGridRowCount": 10, "expandedFlg": 1,"showMode": "card"},
    configureData: {
          uuid: 8604058,
          layoutId: 100222154,
          parentId: 2
    }     
  }
  ```
  
- ####传入参数说明：
 1. componentID:是模块的唯一标示，也是模块state的ID的名称来源。
 2. componentName:是模块的名称，也就是后台定义的widgetType字段的值。
 3. componentInitUrl:是获取模块数据接口的url。
 4. componentInitParame:是模块数据接口需要传的参数。当要获取模块数据的时候直接把此参数做为参数对象传给后台就可以。
 5. attributes:是模块layoutWidgets接口返回的对模块描述的属性数据。
 6. configureData:内部放有uuid,layoutId,parentId三个重要参数，如果有需要使用这三个参数可以从此对象中取。
 
- ####当模块需要其他传入参数时，只需要再App.defaultProps中进行添加即可。


- #### container类说明
  
  此类主要是对模块进行state的筛选传入和模块action的绑定，并对模块state进行多ID的生成。主要是在类的componentWillMont(）生命周期方法中进行state多ID的初始化。如下：
  
 ```javascript
componentWillMount() {
    if (!this.props.state.hasIn(['instances', this.props.componentID])) {
      this.props.actions.initState(this.props.componentID);
    }
  }
  
 ```
 
 state和actions的绑定：
 
 ```javascript
  export default connect(state => ({
      state: state.get('reduxDemo'),//这个地方的state.get()方法里面的参数必须和reducers文件夹里的index.js里面的对reducer的combineReducers(）操作的名称一致，否则会有state为空的报错。
    }),
      (dispatch) => ({
        actions: bindActionCreators(allActions, dispatch)//对action进行绑定。
      })
   )(Container);
   
 ```

当组件需要用到其他组件时，其他组件的state也需要再上面的代码中进行绑定，当自身组件需要调用其他组件的action以此来触发其他组件的render的时候，调用的其他组件的action，也是在上面代码中进行绑定。

对此类中的其他代码都不需要进行改动。
  
  
  
  
  
  
  
  
  
  
  
  
  
  
