### 寻求css架构最佳实践。参照Bootstrap模式。

理想情况：  
**资源库（基础） -> 组件库（黑盒） -> 页面大组件库（面向业务） -> 页面使用**


造枪模式

工厂：
1. 接收枪支需求。或者自己创造需求。
2. 采购原料。原子性。基础材料。
3. 打造最基础的零件。零件通用。
4. 零件组合为枪支的通用部件。以及不同枪支的专用部件。
5. 通用部件和专用部件按原定设计拼接，组成专用枪支。
6. 专用枪支可拆解组合，拆解后可替换部件。不同枪支的通用部件可互相替换，专有部件不可以互相替换。


1. 需求。不同样式页面，风格部分一致。
2. 原料。
    - 变量文件。确定语义化的变量。
    - mixins。功能函数。复用。
    - utilities。工具类。对mixins的直接使用。高一级的抽象。
3. 零件。
    - _alert.scss, _badge.scss。
    - _buttons.scss, _tables.scss
    - 较底层，针对某个非常小的元素。
4. 部件。
    - 提供更多元素的UI区域部件。
    - 弹窗。包含 text, button
    - 轮播图。 包含 image, button，icon, text.
    - 导航bar。包含 button, icon, text
5. 专用枪支。
    - 具体页面。部件组合。
    - 页面通用大组件。
    - 页面专用大组件。


落地到项目中，应该是不同页面都会引入一个通用css， 然后引入一个对应该页面的css.
css文件中类名和html中对应，然后在这个类中从组件库里按需取用。  
这样既保证组件的复用，又保持html结构的简洁，将复杂度存留在css文件内。
如果html中有通用的结构，则也可以将其抽出复用，比如一个弹窗。抽出为页面大组件，


```html
<div class="popover">
    <div class="title">
        <h2>111</h2>
    </div>
    <div class="body">
        <p>22222</p>
    </div>
    <div class="foot">
        <button class="confirm">
            确认
        </button>
        <button class="cancel">
            取消
        </button>
    </div>
</div>

```
结构一旦固定，那在页面大组件库中添加。
甚至如果结构不经常变化，在大组件中不需要写详细类名，直接对应元素tag层级关系写样式就好。
这样html中就不用写很多相同的类名了。
但这样可能html的可读性变差，最好将页面大组件中保持在组件可维护，可读的前提下，类名尽量少。
这里又不好量化。
```
.popover {
  .title {

    h2 {

    }
  }
  .body {

    p {

    }
  }
  .foot {

    .confirm {

    }
    .close {

    }
  }

}



```

探索css最佳开发实践。












