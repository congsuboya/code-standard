
## <a name ="loop">遍历</a>
   - 不要再使用for()这种遍历方式，转到使用map,some

  ```javascript
    
      //let data=[1,2,3,4,5,6]
      //bad
      for(let i=0;i<data.length;i++){
        data[i];
        ...
      }
      
      //bad
      for(let i = 0; i<data.length;i++){
          if(data[i]==3){
            ....
            break;
          }
      }
      
      //good
      data.map((item,index)=>{
        item;
        ...
      })
      
      //good
      data.some((item,index)=>{
        if(item == 3){
          return true;
        }
      })
    ```


## <a name="type-casting--coercion">类型转换</a>

  - 在语句开始时执行类型转换。
  - 字符串：

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    let totalScore = this.reviewScore + '';

    // good
    let totalScore = '' + this.reviewScore;

    // bad
    let totalScore = '' + this.reviewScore + ' total score';

    // good
    let totalScore = this.reviewScore + ' total score';
    ```

  - 使用 `parseInt` 转换数字时总是带上类型转换的基数。

    ```javascript
    let inputValue = '4';

    // bad
    let val = new Number(inputValue);

    // bad
    let val = +inputValue;

    // bad
    let val = inputValue >> 0;

    // bad
    let val = parseInt(inputValue);

    // good
    let val = Number(inputValue);

    // good
    let val = parseInt(inputValue, 10);
    ```

  - 如果因为某些原因 `parseInt` 成为你所做的事的瓶颈而需要使用位操作解决时，留个注释说清楚原因和你的目的。

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    let val = inputValue >> 0;
    ```

  - **注：** 小心使用位操作运算符。数字会被当成 [64 位值](http://es5.github.io/#x4.3.19)，但是位操作运算符总是返回 32 位的整数（[source](http://es5.github.io/#x11.7)）。位操作处理大于 32 位的整数值时还会导致意料之外的行为。最大的 32 位整数是 2,147,483,647：

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  - 布尔:

    ```javascript
    let age = 0;

    // bad
    let hasAge = new Boolean(age);

    // good
    let hasAge = Boolean(age);

    // good
    let hasAge = !!age;
    ```
*[Top](#types)*
*[返回上级](../ji-ben-gui-fan.md)*  