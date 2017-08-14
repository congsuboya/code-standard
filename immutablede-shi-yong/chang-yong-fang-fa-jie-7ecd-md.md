## <a name="object">常用对象</a>

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

## <a name="functions">常用方法</a>


  - **fromJS()**:把一个Object转换为immutable对象
   
    ```javascript
    import { fromJS, Iterable } from 'immutable';
    
    let config ={name:'111',age:18,courses:[1,2,3]}
    let immutableOb = fromJS(config);
    
    Iterable.isImmutable(immutableOb) //true
    
    Iterable.isKeyed(config) //false
    Iterable.isKeyed(immutableOb) //true
    
    Iterable.isKeyed(immutableOb.get('courser')) //false
    Iterable.isIndexed()(immutableOb.get('courser')) //true   
    
    ```
    
    
  - **is()**:判断两个immutable对象的值是否相等
    
 ```javascript
  import { fromJS, Iterable, Map } from 'immutable';
  const map1 = Map({ a: 1, b: 1, c: 1 })
  const map2 = Map({ a: 1, b: 1, c: 1 })
  assert(map1 !== map2)
  assert(Object.is(map1, map2) === false)
  assert(is(map1, map2) === true)
 ```
    
- **isIndexed()**:判断immutable对象的是否是List类型

  ```javascript
  import {  Iterable, List, Map, Set } from 'immutable';
  Iterable.isIndexed([]); // false
  Iterable.isIndexed({}); // false
  Iterable.isIndexed(Map()); // false
  Iterable.isIndexed(List()); // true
  Iterable.isIndexed(Set()); // false
  ```
    
- **isKeyed()**:判断immutable对象的是否是Map类型

   
  ```javascript
  import {  Iterable, List, Map, Set } from 'immutable';
  Iterable.isKeyed()([]); // false
  Iterable.isKeyed()({}); // false
  Iterable.isKeyed()(Map()); // true
  Iterable.isKeyed()(List()); // false
  ```

 - **List.isList()**:判断一个对象是否是immutable 类型的List
 
  ```javascript
  List.isList([]); // false
  List.isList(List()); // true     
  ```

- **set()**:给对象赋值
- List和Map 通用
  
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
  
  
  - **setIn()**:给对象内部对象的value赋值
  - List和Map 通用


  ```javascript
    import { List }  from ('immutable');
    const list = List([ 0, 1, 2, List([ 3, 4 ])])
    list.setIn([3, 0], 999);
    // List [ 0, 1, 2, List [ 999, 4 ] ]
  ```
  
  - **update()**:更新对象的值，能拿到要更新的value
  - List和Map 通用


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
  
  - **updateIn()**:更新对象某个key的对象内部的值，能拿到要更新的value
  - List和Map 通用

  
  ```javascript
    import { List }  from ('immutable');
    const list = List([ 0, 1, 2, List([ 3, 4 ])])
    list.updateIn([3, 0],v => 999);
    // List [ 0, 1, 2, List [ 999, 4 ] ]
  ```

  - **withMutations()**:很重要的一个方法，当你需要改变List或者Map里面多个值得时候使用
  - List和Map 通用
  
  ```javascript
    import { List, Map } from ('immutable');
    const map1 = Map()
    const map2 = map1.withMutations(map => {
        map.set('a', 1).set('b', 2).set('c', 3)
    })
    console.log(map1.size === 0)
    console.log(map2.size === 3)
  ```




*[Top](#object)*
*[返回上级](../immutablede-shi-yong.md)*  



