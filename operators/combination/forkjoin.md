# forkJoin

#### 签名: `forkJoin(...args, selector : function): Observable`

## 当所有 observables 完成时发出每个 observable 的最新值。

---

:bulb:  如果你想要多个 observables 按发出顺序相对应的值的组合，试试 [zip](zip.md)！

---

### 示例

##### 示例 1: 发起可变数量的请求

( [jsBin](http://jsbin.com/taziyomusa/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/5fj77920/) )

```js
const myPromise = val => new Promise(resolve => setTimeout(() => resolve(`Promise Resolved: ${val}`), 5000))

/*
  当所有 observables 完成是，将每个 observable 
  的最新值作为数组发出
*/
const example = Rx.Observable.forkJoin(
  // 立即发出 'Hello'
  Rx.Observable.of('Hello'),
  // 1秒后发出 'World'
  Rx.Observable.of('World').delay(1000),
  // 1秒后发出0
  Rx.Observable.interval(1000).take(1),
  // 以1秒的时间间隔发出0和1
  Rx.Observable.interval(1000).take(2),
  // 5秒后解析 'Promise Resolved' 的 promise
  myPromise('RESULT')
);
//输出: ["Hello", "World", 0, 1, "Promise Resolved: RESULT"]
const subscribe = example.subscribe(val => console.log(val));

// 发起5个请求
const queue = Rx.Observable.of([1,2,3,4,5]);
// 发出包含所有5个结果的数组
const exampleTwo = queue
  .mergeMap(q => Rx.Observable.forkJoin(...q.map(myPromise)));
/*
  输出:
  [
   "Promise Resolved: 1", 
   "Promise Resolved: 2", 
   "Promise Resolved: 3", 
   "Promise Resolved: 4",    
   "Promise Resolved: 5"
  ]
*/
const subscribeTwo = exampleTwo.subscribe(val => console.log(val));
```


### 其他资源

* [forkJoin](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-forkJoin) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/observable/ForkJoinObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/observable/ForkJoinObservable.ts)
