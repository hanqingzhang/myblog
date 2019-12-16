这是面试腾讯2020校招面试的时候遇到的问题

### 1.visibility: hidden;

### 2.display: none;

相同点：都是隐藏标签，对应的标签==仍存在DOM结构中==

不同点：

标签设置display: none后，不会占据该标签原来所在的位置，会触发==重流==。

标签设置visibility: hidden后，仍占据原来的位置，会触发==重绘==。

**联想：
v-if和v-show**

相同点：都可以控制标签的显隐。

一、实现本质方法区别

- v-if是动态的向DOM树内添加或者删除DOM元素
- v-show本质是利用标签的display属性，通过visibility和none控制显隐
- v-if="false"在DOM不能获取到该标签
- v-show=false在DOM中仍能获取到该标签

二、编译的区别

- v-show其实是在控制css
- v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁的重建内部的事件监听和子组件

三、编译的条件

- v-show都会编译，初始值为false,只是将display设为none,但它也编译了
- v-if初始值为false，就不会编译了

四、性能

- v-show只编译一次，后面其实就是控制css，
- 而v-if不停的销毁和创建，故v-show性能更好一点

### 3.opacity: 0;

CSS3属性，设置0可以使一个元素完全透明


### 4.position: absolute;
设置一个很大的 left 负值定位，使元素定位在可见区域之外