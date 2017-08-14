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
  EXAMPLE
    ```javascript
    List.isList([]); // false
    List.isList(List()); // true     
    ```



