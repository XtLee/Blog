# Vue3.0学习笔记-动机与组合式api简介

**本文以vue2.x版本为基础，对比vue3.0的差异进行梳理；**

## Vue3动机

vue3的出现，是为了解决vue2里面，功能代码耦合性过高的问题；

想象一下，在读别人编写的vue2代码的时候，经常出现看一下html，然后拖动到methods部分看一下对应的函数，再去data里看一下用到的数据结构。这样来回跳转、切换浏览位置的方式会严重影响阅读效率。

vue3提供的组合式API完全解决了这个问题。你只需要在需要vue支持的时候调用它所提供的api即可，不会强制要求你必须将逻辑对应的部分放入到对应的功能函数里。

例如：数字点击加一的函数。

```vue
// vue2
<script>
export default {
    data() {
        return {
            num: 1
        }
    },
    methods: {
        numAdd() {
            this.num += 1;
        }
    }
}
</script>

// vue3
<script>
import { ref } from 'vue';
export default {
    setup() {
    	// 数据与逻辑
        const num = ref(1);
        const numAdd = ()=> {
            num.value += 1;
        };

        return {
            num,
            numAdd
        }
    }
}
</script>
```

通过引入需要的api，我可以将数据与逻辑代码写在任何地方，需要在html里用到的只用在`setup`函数内return出来即可；


## Vue3.0组合式Api简介

Api分类 | Vue3 | Vue2 | 描述 | 使用方式 
---|---|---|---|---
生命周期（只能定义在setup函数内） | setup | beforeCreate | vue组件初始化，初始化事件以及生命周期 | setup() {}
| - | setup | created | vue组件初始化，初始化数据监听 | setup() {}
| - | onBeforeMount | beforeMount | 编译html | onBeforeMount(()=> {})
| - | onMounted | mounted | 创建虚拟dom | onMounted(()=> {})
| - | onBeforeUpdate | beforeUpdate | data数据变更 | onBeforeUpdate(()=> {})
| - | onUpdated | updated | 虚拟dom更新并且渲染完毕 | onUpdated(()=> {})
| - | onBeforeUnmount | beforeDestroy | 调用destory()或unmount()时触发 | onBeforeUnmount(()=> {})
| - | onUnmounted | destroyed | 组件销毁时触发 | onUnmounted(()=> {})
数据变量定义 | ref | data | 定义一个被数据监听的变量 | ref(变量内容)
| - | reactive | - | 定义一个被数据监听的变量；同ref的区别是，ref可以作用于基础类型数据，而reactive只能作用于引用类型数据；并且reactive定义的变量一旦解构或展开，将取消数据监听； | reactive(引用类型数据)
| - | toRefs | 无 | 将对象的每个property都转化为相应的ref | toRefs(数据对象)
计算、侦听属性 | watchEffect | watch | 调用时执行一次，依赖改变时再次执行 | watchEffect(()=> {})
| - | watch | watch | 同2.x的watch | watch(数据源，(数据源)=> {执行函数})
| - | computed | computed | 同2.x的computed | computed(()=> 只读的响应式的引用)

