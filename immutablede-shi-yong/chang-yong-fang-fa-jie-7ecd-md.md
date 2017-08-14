## <a name="types">类型</a>

  - **List**: 对应于js中的列表，数组。
  
   + 创建一个List 对象。

    ```javascript
    import { List }  from ('immutable');
    const emptyList = List()
      // List []
      
    const obList = [ 1, 2, 3, 4 ];
    const immutabelList = List(obList);
      
    ```
  - **Map**: 对应于js中的对象。

    + 创建一个Map 对象。

    ```javascript
     import { Map }  from ('immutable');
     Map({ key: "value" });
     Map([ [ "key", "value" ] ]);
     
     let obj = { 1: "one" }
     Object.keys(obj) // [ "1" ]
     obj["1"] // "one"
     obj[1]   // "one"
    
     let map = Map(obj)
     map.get("1") // "one"
     map.get(1)   // undefined
     
    ```

## <a name="types">List常用方法</a>

 - **List.isList()**:判断一个对象是否是immutable 类型的List
 
  例子
    ```javascript
    List.isList([]); // false
    List.isList(List()); // true     
    ```

- **set()**:给List对象赋值

  例子
  ```javascript
  const originalList = List([ 0 ]);
  // List [ 0 ]
  originalList.set(1, 1);
  // List [ 0, 1 ]
  originalList.set(0, 'overwritten');
  // List [ "overwritten" ]
  originalList.set(2, 2);
  // List [ 0, undefined, 2 ]
  
  List().set(50000, 'value').size;
  // 50001
  ```
  
  
  - **setIn()**:给List对象内部对象的value赋值

  例子
  ```javascript
  import { List }  from ('immutable');
  const list = List([ 0, 1, 2, List([ 3, 4 ])])
  list.setIn([3, 0], 999);
  // List [ 0, 1, 2, List [ 999, 4 ] ]
  ```
  
  
  - **update()**:更新List对象的值，能拿到要更新的value

  例子
  ```javascript
  const originalList = List([ 0 ]);
  // List [ 0 ]
  originalList.updata(1,v => 1);
  // List [ 0, 1 ]
  originalList.updata(0,v => 'overwritten');
  // List [ "overwritten" ]
  originalList.updata(2,v => 2);
  // List [ 0, undefined, 2 ]
  
  ```
  
  
  - **updateIn()**:更新List对象某个key的对象内部的值，能拿到要更新的value

  例子
  ```javascript
  import { List }  from ('immutable');
  const list = List([ 0, 1, 2, List([ 3, 4 ])])
  list.updateIn([3, 0],v => 999);
  // List [ 0, 1, 2, List [ 999, 4 ] ]
  ```











