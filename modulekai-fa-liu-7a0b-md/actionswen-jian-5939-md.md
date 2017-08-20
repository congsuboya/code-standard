## actions文件夹说明
> 此文件夹内有三个类一个是index.js,一个是actions.js以及actionType.js

- ####index类说明

  此类不需要进行任何改动。
  
- ####actions类说明
此类中主要是对开发模块的action进行定义，此类中有三个方法的定义。
  1. initState(）方法是对State多ID的初始化调用的方法，要进行保留，如果外界传入的参数需要写入state的，直接在此方法中添加参数进行改造即可。
  2. clearState() 方法是当组件销毁时调用的方法，对组件的state对应的销毁Id下面的数据进行删除，以免state过于庞大。
  3. click（） 方法是redux中普通action定义的demo,模块的所有action定义可以模仿此方法来进行定义。注意一点所有定义的action方法必须传入此组件的componentID，即时此方法中的Id。此方法可以删除。
  4. getModuleData() 方法是调用网络的demo方法，同时也是获得模块数据的方法，此方法必备，不能删除。此方法中的参数分别是传入模块的componentInitUrl,componentInitParame,configureData以及最后的componentID。
  
 ```javascript
     export function getModuleData(urlStr, param,  configData, Id) {
        return async function (dispatch, getState) {
            return useCacheThenNet(urlStr, param,
                (response) => {
                    let json = JSON.parse(response);
                    if (json&&json.status&&json.status == '0'&&json.data) {
                        let dataBody = json['data'][configData.uuid]['data'];
                        dispatch(dateSucess(dataBody,Id))
                    } else {
                        dispatch(dateSucess(Id))
                    }
                }).catch((error) => {
                    dispatch(dateError(Id));
                    Toast.showShortBottom(getLocalString('loadError'));
                });
        }
    }

    ```


 
  
  
  
  
  
  
  
  
  
  
  
  
  
  
