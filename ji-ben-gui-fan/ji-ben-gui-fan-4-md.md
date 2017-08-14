## <a name="naming-conventions">命名规则</a>

  - 避免单字母命名。命名应具备描述性。

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - 使用驼峰式命名对象、函数和实例。

    ```javascript
    // bad
    let OBJEcttsssss = {};
    let this_is_my_object = {};
    let o = {};
    function c() {}

    // good
    let thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  - 使用帕斯卡式命名构造函数或类。
  > 帕斯卡式命名 : 每一个单字的首字母都采用大写字母的命名格式，被称为“Pascal命名法”，源自于Pascal语言的命名惯例，也有人称之为“大驼峰式命名法”（Upper Camel Case）。

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    let bad = new user({
      name: 'nope'
    });

    // good
    function User(options) {
      this.name = options.name;
    }

    let good = new User({
      name: 'yup'
    });
    ```

  - 不要使用下划线前/后缀。

  > 为什么？JavaScript 并没有私有属性或私有方法的概念。虽然使用下划线是表示「私有」的一种共识，但实际上这些属性是完全公开的，它本身就是你公共接口的一部分。这种习惯或许会导致开发者错误的认为改动它不会造成破坏或者不需要去测试。长话短说：如果你想要某处为「私有」，它必须不能是显式提出的。

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // good
    this.firstName = 'Panda';
    ```

  - 不要保存 `this` 的引用。使用 Function#bind。类里面的方法需要用到this的统一再类的构造方法里面进行绑定即bind,不要再调用这个方法的地方进行绑定.

    ```javascript
    
    // good
    class Demo extends React.Component{
    
      constructor(props) {
        super(props);
        //good
        this.Add = this.Add.bind(this)
      }
      
      //good
      Add () {
        return function () {
          console.log(this);
        };
      }
    
      // bad
      Add1 () {
        let self = this;
        return function () {
          console.log(self);
        };
      }
    
      render(){
        this.Add();
        //bad
        this.Add1.bind(this)();
        return(
          ...
        )
      }
      
     ...
    }

    ```

  - 如果你的文件导出一个类，你的文件名应该与类名完全相同。
    ```javascript
    // file contents
    class CheckBox {
      // ...
    }
    edport default CheckBox;

    // in some other file
    // bad
    import CheckBox from './checkBox';

    // bad
    import CheckBox from './check_box';

    // good
    import CheckBox from './CheckBox';
    ```


## <a name="accessors">存取器</a>

  - 属性的存取函数不是必须的。
  - 如果你需要存取函数时使用 `getVal()` 和 `setVal('hello')`。

    ```javascript
    // bad
    dragon.age();

    // good
    dragon.getAge();

    // bad
    dragon.age(25);

    // good
    dragon.setAge(25);
    ```

  - 如果属性是布尔值，使用 `isVal()` 或 `hasVal()`。

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

*[Top](#types)*
*[返回上级](../ji-ben-gui-fan.md)*  