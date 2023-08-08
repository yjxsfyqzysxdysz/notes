# Vuex从使用到原理解析

**一、Vuex是什么**

Vuex是专门为Vuejs应用程序设计的**状态管理工具**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

**1、Vuex的构成**



![img](https://pic4.zhimg.com/80/v2-f330e46f1a97cfe60b8914802688083b_720w.jpg)



由上图，我们可以看出Vuex有以下几个部分构成：

**1）state**

state是存储的单一状态，是存储的基本数据。

**2）Getters**

getters是store的计算属性，对state的加工，是派生出来的数据。就像computed计算属性一样，getter返回的值会根据它的依赖被缓存起来，且只有当它的依赖值发生改变才会被重新计算。

**3）Mutations**

mutations提交更改数据，使用store.commit方法更改state存储的状态。（mutations同步函数）

**4）Actions**

actions像一个装饰器，提交mutation，而不是直接变更状态。（actions可以包含任何异步操作）

**5）Module**

Module是store分割的模块，每个模块拥有自己的state、getters、mutations、actions。

```text
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```

**6）辅助函数**

Vuex提供了mapState、MapGetters、MapActions、MapMutations等辅助函数给开发在vm中处理store。

**2、Vuex的使用**



![img](https://pic1.zhimg.com/80/v2-90437dee8c4d7b465b2d0e6e07778ff0_720w.png)



```text
import Vuex from 'vuex';
Vue.use(Vuex); // 1. vue的插件机制，安装vuex
let store = new Vuex.Store({ // 2.实例化store，调用install方法
    state,
    getters,
    modules,
    mutations,
    actions,
    plugins
});
new Vue({ // 3.注入store, 挂载vue实例
    store,
    render: h=>h(app)
}).$mount('#app');
```

**二、Vuex的设计思想**

Vuex的设计思想，借鉴了Flux、Redux，将数据存放到全局的store，再将store挂载到每个vue实例组件中，利用Vue.js的细粒度数据响应机制来进行高效的状态更新。

看了Vuex设计思想，心里难免会有这样的疑问：

+ vuex的store是如何挂载注入到组件中呢？
+ vuex的state和getters是如何映射到各个组件实例中响应式更新状态呢？

**三、Vuex的原理解析**

我们来看下vuex的源码，分析看看上面2个疑惑的问题：

**疑问1：vuex的store是如何挂载注入到组件中呢？**

1、在vue项目中先安装vuex，核心代码如下：

```text
import Vuex from 'vuex';
Vue.use(vuex);// vue的插件机制
```

2、利用vue的[插件机制](https://link.zhihu.com/?target=https%3A//cn.vuejs.org/v2/guide/plugins.html)，使用Vue.use(vuex)时，会调用vuex的install方法，装载vuex，install方法的代码如下：

```text
export function install (_Vue) {
  if (Vue && _Vue === Vue) {
    if (process.env.NODE_ENV !== 'production') {
      console.error(
        '[vuex] already installed. Vue.use(Vuex) should be called only once.'
      )
    }
    return
  }
  Vue = _Vue
  applyMixin(Vue)
}
```

3、applyMixin方法使用vue[混入机制](https://link.zhihu.com/?target=https%3A//cn.vuejs.org/v2/guide/mixins.html)，vue的生命周期beforeCreate钩子函数前混入vuexInit方法，核心代码如下：

```text
Vue.mixin({ beforeCreate: vuexInit });

function vuexInit () {
    const options = this.$options
    // store injection
    if (options.store) {
      this.$store = typeof options.store === 'function'
        ? options.store()
        : options.store
    } else if (options.parent && options.parent.$store) {
      this.$store = options.parent.$store
    }
}
```

分析源码，我们知道了vuex是利用vue的mixin混入机制，在beforeCreate钩子前混入vuexInit方法，vuexInit方法实现了store注入vue组件实例，并注册了vuex store的引用属性$store。store注入过程如下图所示：

![img](https://pic4.zhimg.com/80/v2-a8b969f8771a1fc13b7cedfdfe86f0e7_720w.jpg)



**疑问2：vuex的state和getters是如何映射到各个组件实例中响应式更新状态呢？**

store实现的源码在src/store.js

1、我们在源码中找到resetStoreVM核心方法：

```text
function resetStoreVM (store, state, hot) {
  const oldVm = store._vm

  // 设置 getters 属性
  store.getters = {}
  const wrappedGetters = store._wrappedGetters
  const computed = {}
  // 遍历 wrappedGetters 属性
  forEachValue(wrappedGetters, (fn, key) => {
    // 给 computed 对象添加属性
    computed[key] = partial(fn, store)
    // 重写 get 方法
    // store.getters.xx 其实是访问了store._vm[xx]，其中添加 computed 属性
    Object.defineProperty(store.getters, key, {
      get: () => store._vm[key],
      enumerable: true // for local getters
    })
  })

  const silent = Vue.config.silent
  Vue.config.silent = true
  // 创建Vue实例来保存state，同时让state变成响应式
  // store._vm._data.$$state = store.state
  store._vm = new Vue({
    data: {
      $$state: state
    },
    computed
  })
  Vue.config.silent = silent

  // 只能通过commit方式更改状态
  if (store.strict) {
    enableStrictMode(store)
  }
}
```

从上面源码，我们可以看出

+ Vuex的state状态是响应式，是借助vue的data是响应式，将state存入vue实例组件的data中；
+ Vuex的getters则是借助vue的计算属性computed实现数据实时监听。

computed计算属性监听data数据变更主要经历以下几个过程：

![img](https://pic3.zhimg.com/80/v2-2730644102b66eef140110b814a90496_720w.jpg)



**小结**

Vuex是通过全局注入store对象，来实现组件间的状态共享。在大型复杂的项目中（多级组件嵌套），需要实现一个组件更改某个数据，多个组件自动获取更改后的数据进行业务逻辑处理，这时候使用vuex比较合适。假如只是多个组件间传递数据，使用vuex未免有点大材小用，其实只用使用组件间常用的通信方法即可。