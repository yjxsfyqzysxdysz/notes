# Hash、History、Memory路由——Vue-Router源码

## 前言

在了解路由之前先了解路由及路由器的概念。

**路由**（routing）：就是通过互联的网络把信息从源地址传输到目的地址的活动；路由通常根据**路由表**——一个存储到各个目的地的最佳路径的表——来引导*分组转送*。做成硬件之后就是**路由器**。

## hash 模式

hash模式代码： [codesandbox.io/s/x3nxq950k…](https://codesandbox.io/s/x3nxq950ko)

点击，在URL里会添加以`#`开头的字段，可通过`window.location.hash`获取该字符段，`hashchange`事件可监听hash值改变。

**优点**：完全前端路由，只改变#后面值，无刷新。

**缺点**：不会出现在HTTP请求中，SEO不友好。

## history 模式

history模式代码： [codesandbox.io/s/oqjvqm6w0…](https://codesandbox.io/s/oqjvqm6w05)

1. 通过`window.location.pathname`获取`/`路径字段，
2. 通过`history.back()`、`history.go()`、`history.forward()`完成后退前进等操作，
3. 在HTML5新增了`pushState`、`replaceState`，通过`window.history.pushState(stateObject,title,url)`将路由添加到历史堆栈中去，`replaceState()`修改历史堆栈的记录，可通过`history.state`查看当前状态记录，但这只是修改了URL的路径，不会加载刷新页面，`window.onpopstate`对状态监听，但只会在浏览器的前进、后退按钮或者JavaScript的`history.back()、history.go()、history.forward()`方法中触发。

**优点**：在同源的情况下，实现了前端完全自由，stateObject可以是任何数据类型，URL可以是相对路径也可以是绝对路径。

**缺点**：如果后端没有做对应的路由，在刷新时会出现404。

## memory 模式

memory模式代码： [codesandbox.io/s/936269l69…](https://codesandbox.io/s/936269l69o)

该模式就是将路由存在一个对象里，在URL里看不到对应的路径，适用于手机端，但使用很少。

## Vue-Router

相当于一个`a`标签，`to`相当于`href`属性。 则是展示的内容。

**VueRouter原理** [源码](https://github.com/vuejs/vue-router/blob/dev/dist/vue-router.js)

源码扫了一遍，看着确实为难，但了解了大概思路，

1. 首先是封装了RouterView

   只接受一个name属性

   ![img](https://user-gold-cdn.xitu.io/2020/7/8/1732a51d22f974b8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

   render函数return一个h(component, data, children)，其实就是创建要渲染的组件，只不过中间对component组件、data对象、children子集做了一些处理。

   

2. 再者是封装了RouterLink

   包含to、tag、activeClass、event等属性

   ![img](https://user-gold-cdn.xitu.io/2020/7/8/1732a3006691ddea?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

   

LinK的render最终return的是`h(this.tag, data, this.$slots.default)`，相当于默认创建了一个a标签，只是对a标签做了如下事件监听

```
//执行的函数，调用了replace或者push方法
    var handler = function (e) {
        if (guardEvent(e)) {
          if (this$1.replace) {
            router.replace(location, noop);
          } else {
            router.push(location, noop);
          }
        }
    };
    
//默认监听click事件
    var on = { click: guardEvent };

//对传入事件判断并监听
    if (Array.isArray(this.event)) {
        this.event.forEach(function (e) {
          on[e] = handler;
        });
    } else {
        on[this.event] = handler;
    }
```

1. 封装VueRouter

```
var VueRouter = function VueRouter (options) {
  if ( options === void 0 ) options = {};

  this.app = null;
  this.apps = [];
  this.options = options;
  this.beforeHooks = [];
  this.resolveHooks = [];
  this.afterHooks = [];
  this.matcher = createMatcher(options.routes || [], this);

//模式默认为‘hash’模式，可通过mode定义
  var mode = options.mode || 'hash';
  this.fallback = mode === 'history' && !supportsPushState && options.fallback !== false;
  if (this.fallback) {
    mode = 'hash';
  }
  if (!inBrowser) {
    mode = 'abstract';
  }
  this.mode = mode;

  switch (mode) {
    case 'history':
      this.history = new HTML5History(this, options.base);
      break
    case 'hash':
      this.history = new HashHistory(this, options.base, this.fallback);
      break
    case 'abstract':
      this.history = new AbstractHistory(this, options.base);
      break
    default:
      if (process.env.NODE_ENV !== 'production') {
        assert(false, ("invalid mode: " + mode));
      }
  }
};
```

VueRouter.prototype上添加了go、back、forward等方法

```
function createMatcher (
  routes,  //创建的路由表
  router  //new VueRouter实例
) {
  var ref = createRouteMap(routes);
  var pathList = ref.pathList;
  var pathMap = ref.pathMap;
  var nameMap = ref.nameMap;

  //创建addRoutes函数，动态添加路由
  function addRoutes (routes) {
    //*路由映射
    createRouteMap(routes, pathList, pathMap, nameMap);
  }

  //创建match函数，匹配路由
  function match (
    raw,
    currentRoute,
    redirectedFrom
  ) {
    var location = normalizeLocation(raw, currentRoute, false, router);
    var name = location.name;

    if (name) {
      var record = nameMap[name];
      if (process.env.NODE_ENV !== 'production') {
        warn(record, ("Route with name '" + name + "' does not exist"));
      }
      if (!record) { return _createRoute(null, location) }
      var paramNames = record.regex.keys
        .filter(function (key) { return !key.optional; })
        .map(function (key) { return key.name; });

      if (typeof location.params !== 'object') {
        location.params = {};
      }

      if (currentRoute && typeof currentRoute.params === 'object') {
        for (var key in currentRoute.params) {
          if (!(key in location.params) && paramNames.indexOf(key) > -1) {
            location.params[key] = currentRoute.params[key];
          }
        }
      }

      location.path = fillParams(record.path, location.params, ("named route \"" + name + "\""));
      return _createRoute(record, location, redirectedFrom)
    } else if (location.path) {
      location.params = {};
      for (var i = 0; i < pathList.length; i++) {
        var path = pathList[i];
        var record$1 = pathMap[path];
        if (matchRoute(record$1.regex, location.path, location.params)) {
          return _createRoute(record$1, location, redirectedFrom)
        }
      }
    }
    // no match
    return _createRoute(null, location)
  }

  //重定向
  function redirect (record,location) {...}
  
  //别名
  function alias (record,location,matchAs) {...}

  function _createRoute (
    record,
    location,
    redirectedFrom
  ) {
    if (record && record.redirect) {
      return redirect(record, redirectedFrom || location)
    }
    if (record && record.matchAs) {
      return alias(record, location, record.matchAs)
    }
    return createRoute(record, location, redirectedFrom, router)
  }

  return {
    match: match,
    addRoutes: addRoutes
  }
}
```

createMatcher 就是暴露出两个方法给VueRouter，需要做路由的映射以及动态添加路由的方法。



[Hash、History、Memory路由——Vue-Router源码](https://juejin.im/post/6847902220873105421)