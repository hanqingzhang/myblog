一个src文件夹和一个index.js，src文件夹放组件，index.js注册组件并导出

分析从三个方面着手：DOM结构，数据属性，事件

1.DOM结构：

```
<button></button>
```
2.数据属性

1)props获取
2)引用computed的属性

3.事件

这里涉及到父子组件通信，子组件向父组件发消息可以用emit实现，父组件监听即可，一般情况下父组件监听的事件名都是自定义的，这里特殊了点，父组件直接监听了“click”事件，谁让button通常就一个点击事件呢

学习点：

1）样式绑定

```
:class="[
      type ? 'el-button--' + type : '',
      buttonSize ? 'el-button--' + buttonSize : '',
      {
        'is-disabled': buttonDisabled,
        'is-loading': loading,
        'is-plain': plain,
        'is-round': round,
        'is-circle': circle
      }
    ]"
```
class的绑定

绑定的class做了归类，boolean类型的归为了一类，放到对象中，我们是不是也可以这样写，让代码更整齐呢
https://cn.vuejs.org/v2/guide/class-and-style.html#%E6%95%B0%E7%BB%84%E8%AF%AD%E6%B3%95

2）插槽

插槽就是子组件中的提供给父组件使用的一个占位符，用<slot></slot> 表示，父组件可以在这个占位符中填充任何模板代码，如 HTML、组件等，填充的内容会替换子组件的<slot></slot>标签。
```
 <span v-if="$slots.default"><slot></slot></span>
```

https://www.cnblogs.com/mandy-dyf/p/11528505.html
https://cn.vuejs.org/v2/api/#vm-slots

附源码

```
<template>
  <button
    class="el-button"
    @click="handleClick"
    :disabled="buttonDisabled || loading"
    :autofocus="autofocus"
    :type="nativeType"
    :class="[
      type ? 'el-button--' + type : '',
      buttonSize ? 'el-button--' + buttonSize : '',
      {
        'is-disabled': buttonDisabled,
        'is-loading': loading,
        'is-plain': plain,
        'is-round': round,
        'is-circle': circle
      }
    ]"
  >
    <i class="el-icon-loading" v-if="loading"></i>
    <i :class="icon" v-if="icon && !loading"></i>
    <span v-if="$slots.default"><slot></slot></span>
  </button>
</template>
<script>
  export default {
    name: 'ElButton',

    inject: {
      elForm: {
        default: ''
      },
      elFormItem: {
        default: ''
      }
    },

    props: {
      type: {
        type: String,
        default: 'default'
      },//类型	string	primary / success / warning / danger / info / text
      size: String, //尺寸	string	medium / small / mini
      icon: {
        type: String,
        default: ''
      },
      nativeType: {
        type: String,
        default: 'button'
      },
      loading: Boolean,
      disabled: Boolean,
      plain: Boolean,
      autofocus: Boolean,
      round: Boolean,
      circle: Boolean
    },

    computed: {
      _elFormItemSize() {
        return (this.elFormItem || {}).elFormItemSize;
      },
      buttonSize() {
        return this.size || this._elFormItemSize || (this.$ELEMENT || {}).size;
      },
      buttonDisabled() {
        return this.disabled || (this.elForm || {}).disabled;
      }
    },

    methods: {
      handleClick(evt) {
        this.$emit('click', evt);
      }
    }
  };
</script>

```
