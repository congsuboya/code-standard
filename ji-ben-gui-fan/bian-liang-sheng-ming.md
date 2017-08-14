## <a name="types">类型</a>

  - **原始值**: 存取直接作用于它自身。

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    let foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
  - **复杂类型**: 存取时作用于它自身值的引用。

    + `object`
    + `array`
    + `function`

    ```javascript
    let foo = [1, 2];
    let bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```


## <a name="objects">对象</a>

  - 使用直接量创建对象。

    ```javascript
    // bad
    let item = new Object();

    // good
    let item = {};
    ```

  - 使用同义词替换需要使用的保留字。

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    };

    // bad
    var superman = {
      klass: 'alien'
    };

    // good
    var superman = {
      type: 'alien'
    };
    ```

## <a name="arrays">数组</a>

  - 使用直接量创建数组。

    ```javascript
    // bad
    let items = new Array();

    // good
    let items = [];
    ```

  - 向数组增加元素时使用 Array#push 来替代直接赋值。
  

    ```javascript
    let someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  - 当你需要拷贝数组时，使用 Array#slice。

    ```javascript
    let itemsCopy = [];

    // bad
    items.map((item,index)=>{
      itemsCopy.push(item)
    })

    // good
    itemsCopy = items.slice();
    ```


## <a name="strings">字符串</a>

  - 使用单引号 `''` 包裹字符串。

    ```javascript
    // bad
    let name = "Bob Parr";

    // good
    let name = 'Bob Parr';

    // bad
    let fullName = "Bob " + this.lastName;

    // good
    let fullName = 'Bob ' + this.lastName;
    ```

  - 超过100个字符的字符串应该使用连接符写成多行。
  - 注：若过度使用，通过连接符连接的长字符串可能会影响性能。

    ```javascript
    // bad
    let errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    let errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    let errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```


## <a name="functions">函数</a>

  - 函数表达式：

    ```javascript
    // 匿名函数表达式
    let anonymous = function() {
      return true;
    };

    // 命名函数表达式
     named() {
      return true;
    };

    ```

  - 永远不要把参数命名为 `arguments`。这将取代函数作用域内的 `arguments` 对象。

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```


## <a name="properties">属性</a>

  - 使用 `.` 来访问对象的属性。

    ```javascript
    let luke = {
      jedi: true,
      age: 28
    };

    // bad
    let isJedi = luke['jedi'];

    // good
    let isJedi = luke.jedi;
    ```

  - 当通过变量访问属性时使用中括号 `[]`。

    ```javascript
    //  let itemsData = json['data'][configData.uuid]['data'];
    
    let uuid = 9869
    let result = {
        data:{
         9869 :{
              ...
              }
          }
        status: 0
    };

    let pageData = result.data[uuid];
    ```


## <a name="variables">变量</a>

  - 类内部总是使用 `let` 来声明变量。外部如果是静态变量使用 `const` 来声明,并且基本数据类型的声明劲量用大写。

    ```javascript
    // bad
    let windowHeight = 100
    class Demo extends React.Component{
      ...
      const tempData = 123
      ...
    }

    // good
    const WINDOW_HEIGHT = 100
    class Demo extends React.Component{
    ...
    let tempData = 123
    ...
    }
    ```

  - 最后再声明未赋值的变量。当你需要引用前面的变量赋值时这将变的很有用。

    ```javascript
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    let items = getItems();
    let dragonball;
    let goSportsTeam = true;
    let len;

    // good
    let items = getItems();
    let goSportsTeam = true;
    let dragonball,length,i;
    ```

  - 在作用域顶部声明变量。这将帮你避免变量声明提升相关的问题。

    ```javascript
    // bad
    function () {
      test();
      console.log('doing stuff..');

      //..other stuff..

      let name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // good
    function () {
      let name = getName();

      test();
      console.log('doing stuff..');

      //..other stuff..

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // bad - 不必要的函数调用
    function () {
      let name = getName();

      if (!arguments.length) {
        return false;
      }

      this.setFirstName(name);

      return true;
    }

    // good
    function () {
      let name;
      if (!arguments.length) {
        return false;
      }

      name = getName();
      this.setFirstName(name);

      return true;
    }
    ```



*[返回目录](./ji-ben-gui-fan.md)*

