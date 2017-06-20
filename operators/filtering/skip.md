# skip

#### 签名: `skip(the: Number): Observable`

## 跳过N个(由参数提供)发出值。

### 示例

##### 示例 1: 在发送前跳过N个值

( [jsBin](http://jsbin.com/hacepudabi/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/ar1eqbya/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
// 跳过前5个发出值
const example = source.skip(5);
// 输出: 5...6...7...8........
const subscribe = example.subscribe(val => console.log(val));
```


### 其他资源

* [skip](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-skip) :newspaper: - 官方文档
* [过滤操作符: take, first, skip](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/skip.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/skip.ts)
