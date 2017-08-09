## <a name="events">事件</a>

  - 当给事件附加数据时（无论是 DOM 事件还是私有事件），传入一个哈希而不是原始值。这样可以让后面的贡献者增加更多数据到事件数据而无需找出并更新事件的每一个处理器。例如，不好的写法：

    ```js
    // bad
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function (e, listingId) {
      // do something with listingId
    });
    ```

    更好的写法：

    ```js
    // good
    $(this).trigger('listingUpdated', { listingId : listing.id });

    ...

    $(this).on('listingUpdated', function (e, data) {
      // do something with data.listingId
    });
    ```

  **[⬆ 回到顶部](#table-of-contents)**


## <a name="modules">模块</a>

  - 模块应该以 `!` 开始。这样确保了当一个不好的模块忘记包含最后的分号时，在合并代码到生产环境后不会产生错误。[详细说明](https://github.com/airbnb/javascript/issues/44#issuecomment-13063933)
  - 文件应该以驼峰式命名，并放在同名的文件夹里，且与导出的名字一致。
  - 增加一个名为 `noConflict()` 的方法来设置导出的模块为前一个版本并返回它。
  - 永远在模块顶部声明 `'use strict';`。

    ```javascript
    // fancyInput/fancyInput.js

    !function (global) {
      'use strict';

      var previousFancyInput = global.FancyInput;

      function FancyInput(options) {
        this.options = options || {};
      }

      FancyInput.noConflict = function noConflict() {
        global.FancyInput = previousFancyInput;
        return FancyInput;
      };

      global.FancyInput = FancyInput;
    }(this);
    ```

**[⬆ 回到顶部](#table-of-contents)**


## <a name="jquery">jQuery</a>

  - 使用 `$` 作为存储 jQuery 对象的变量名前缀。

    ```javascript
    // bad
    var sidebar = $('.sidebar');

    // good
    var $sidebar = $('.sidebar');
    ```

  - 缓存 jQuery 查询。

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

  - 对 DOM 查询使用层叠 `$('.sidebar ul')` 或 父元素 > 子元素 `$('.sidebar > ul')`。 [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
  - 对有作用域的 jQuery 对象查询使用 `find`。

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

**[⬆ 回到顶部](#table-of-contents)**


## <a name="ecmascript-5-compatibility">ECMAScript 5 兼容性</a>

  - 参考 [Kangax](https://twitter.com/kangax/) 的 ES5 [兼容表](http://kangax.github.com/es5-compat-table/).

**[⬆ 回到顶部](#table-of-contents)**
