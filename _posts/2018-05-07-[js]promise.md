什么叫promise 解决什么问题
典型的有三个状态:  resolved rejected pending

promise实现有很多种 es6 -> Promise

promise解决的问题有
- 回调地域
- 解决同步并发异步在同一时刻内获取并发的结果
- 链式调用

> promise中放了一个函数， 函数executor 执行器
> resolve和reject都是函数，调用后可以让状态进行改变

```javascript
let p = new Promise(function(resolve, reject){
    console.log(1);
    resolve(20); //默认只会执行第一个方法,后面的会被忽略
    reject(20);
})
console.log(2);
//1 2

```

> 所有的Promise的executor都是同步执行的
> 每个promise上都有一个then方法，then方法有两个参数,一个成功的处理函数，一个失败的处理函数

```javascript
p.then(function(data){
    console.log('success', data);
}, function(err){
    console.log('error', err);
})
```

例子: 抛硬币 正：买包 反：不买

```javascript
flipCoin(buy, noBuy) {
    setTimeout(()=> {
        if (Math.random()>0.5) {
            buy();
        } else {
            noBuy();
        }
    }, 2000);
}
let fn = () => {
    console.log('买');
}
let noBuy = () => {
    console.log('不买');
}
flipCoin(buy, noBuy);

function flipCoin() {
    return new Promise(function(resolve, reject){
        setTimeout(()=> {
            if (Math.random()>0.5) {
                resolve();
            } else {
                reject();
            }
        }, 2000);
    });
}

flipCoin().then((data)=>{
    console.log('买');
}, (err)=>{
    console.log('不买');
});

```

> 需求: 读取一个文件1.txt 文件中存的是2.txt 再读取2.txt 读取2.txt的结果“我很帅”

```javascript
let fs = require('fs');
//回调地域, 第二次请求是基于第一次的
// fs.readFile('1.txt', 'utf8', function(err, data){
//     if (err) return console.log(err);
//     console.log(data);
//     fs.readFile(data, 'utf8', function(err, data){
//         if (err) return console.log(err);
//         console.log(data);
//     });
// })

function read(path) {
    return new Promise((resolve, reject)=>{
        fs.readFile(path, 'utf8', function(err, data){
            if(err) return reject(err);
            resolve(data);
        });
    })
}
read('1.txt').then(function(data){
    return read(data); //再次返回promise, 如果是return 1返回的不是promise都认为是成功的
}, (err)=> {
    console.log(err);
    //如果return 100, 则会走到下一个then的成功
    //throw error(), 走到下一个then的失败
}).then((data)=>{
    console.log(data);
}, (err)=>{
    console.log(err);
});
```

> - 如果第一个promise执行完的结果返回的依旧是promise就可以实现链式调用,如果返回失败就执行失败的函数
> - promise第一次then无论返回的是什么（不是promise）都会作为下一次then的成功态
> - 执行时发生了错误也会走到失败
> - catch可以捕获Promise中的错误, 如果相邻的捕获了就不会走到catch

> 使用catch统一处理error

```javascript
read('1.txt').then(function(data){
    return read(data); //再次返回promise, 如果是return 1返回的不是promise都认为是成功的
}).then((data)=>{
    console.log(data);
}).catch(err=>{
    console.log(err); //有错误都走这里
});

//自己有error就走自己的，没有就走catch
read('1.txt').then(function(data){
    return read(data); //再次返回promise, 如果是return 1返回的不是promise都认为是成功的
}, err=>{
    console.log('here', err);//有错误就走这里，不走catch
}).then((data)=>{
    console.log(data);
}).catch(err=>{
    console.log(err);
});

//
read('1.txt').then(function(data){
    return read(data); //再次返回promise, 如果是return 1返回的不是promise都认为是成功的
}).then((data)=>{
    console.log(data);
}).catch(err=>{
    console.log(err); //有错误都走这里
}).then((data)=>{
    console.log('hahah'); //如过有错误也会走到这里，因为没有返回值，被认为是下一个then的成功态
});
```


> Promise.resolve Promise.reject

```javascript
read('1.txt').then(function(data){
    return read(data); //再次返回promise, 如果是return 1返回的不是promise都认为是成功的
}).then((data)=>{
   return Promise.reject(data); //把任何一个东西包装成promise
}).then((data)=>{
    console.log('hahah');
}, err=>{
    console.log('error');
});

```


> all方法会再次返回一个promise实例, 如果数组中的promise有一个失败了,这个promise就失败了，如果都成功了才算成功

```javascript
fs.readFile('./1.txt', 'utf8', function(data, err){
    console.log(data);
})

fs.readFile('./2.txt', 'utf8', function(data, err){
    console.log(data);
})

Promise.all([read('1.txt', read('2.txt'))]).then((data)=>{
    console.log(data);
}, (err)=>{
    console.log('error');
})
```

> race谁先回来就用谁的

```javascript
Promise.race([read('1.txt'), read('2.txt')]).then((data)=>{
    console.log(data);
}, (err)=>{
    console.log('error');
})
```
