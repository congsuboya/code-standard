## <a name="types">类型</a>

  - **List**: 对应于js中的列表，数组。
   + 创建一个List

    ```javascript
    import { List }  from ('immutable');
    const emptyList = List()
      // List []
      
    const obList = [ 1, 2, 3, 4 ];
    const immutabelList = List(obList);
      
    ```
  - **Map**: 对应于js中的对象。

    + `object`
    + `array`
    + `function`

    ```javascript
    let foo = [1, 2];
    let bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```


