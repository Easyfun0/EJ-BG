---
layout: post
title:  "JS-promise"
date:   2022-03-31
author: Easyfun
categories: Javascript
cover:  "/assets/sea.jpg"
---

## JS-Promise

Promise 是一個根據附加給他的 Callback 回傳的物件，以取代傳遞 Callback 到這個函數。
透過then或catch去接收或捕捉非同步結果，主要有三個狀態

1.pending

2.fullfilled

3.rejected

當你用new Promise 內的函式會立即被執行，pending是一開始的狀態，fullfilled只要滿足後，promise會執行resolve的方法，要是失敗就執行rejected的方法。


## 範例一
    function Task(success, time) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                if (success) {
                    resolve(time);
                } else {
                    reject(time);
                }
            }, time);
        });
    }
    // 當前面的Promise的 resolve得到內容後，才會執行.then
    Promise.all([
        Task(true, 1000),
        Task(true, 3000),
        Task(true, 2000)
    ]).then(data => {
        console.log("ok:", data);
    }, err => {
        console.log("err:", err);
    });

執行後會先在pending狀態
![alt text]({{ site.baseurl }}/assets/promise1.jpg "Profile Picture"){:.profile}

下面的Promise在非同步同時完成

在3秒後出現。
![alt text]({{ site.baseurl }}/assets/promise2.jpg "Profile Picture"){:.profile}

---

## 範例二

以下拆解在 Promise 中 new 另一個 Promise

        const myPromise = new Promise((resolve, reject) => {
        console.log('In first Promise, start callback');
        setTimeout(() => {
            let data = 10;
            resolve(data); // =2 秒後執行
            console.log('In fist Promise, resolve data');
        }, 1500);
        });

執行後會先在pending狀態，並且立即執行
![alt text]({{ site.baseurl }}/assets/promise2-2.jpg "Profile Picture"){:.profile}

---

當前面 Promise 的 resolve 得到內容後，才會執行 .then

        myPromise
        .then((value) => {
            console.log('In first then, the value is ' + value);
            return value + 3;
        })
        .then((value) => {
            console.log('In second then, the value is ' + value);
            console.log('In second Promise, start callback');

兩秒後印出，在.then 的 resolvedCallback 中，可以得到在 new Promise 中 resolve 內所得到的值（value）。

下一個.then的resolvedCallback可以取得上一個.then的return值

![alt text]({{ site.baseurl }}/assets/promise2-3.jpg "Profile Picture"){:.profile}


---

如果我們在 .then去return 另一個 new Promise

        return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(value + 3);
            console.log('In second Promise, resolve data');
        }, 2000);
        });
    })

則下一個 .then 會等到這個 Promise 中的 resolve 得到值後才執行。

        .then((value) => {
            console.log('In third then, the value is ' + value);
        })
        .catch((reason) => {
            console.log('Request Failed ' + reason);
        });

兩秒過後，.then 的 resolvedCallback 中，可以得到上一個 new Promise 中 resolve 的值

![alt text]({{ site.baseurl }}/assets/promise2-4.jpg "Profile Picture"){:.profile}

## 總結

會產生非同步的方法有很多，但最常見的非同步處理就是Promise，ES6提供將非同步行為統一相同界面接口，透過then或catch去接收或捕捉非同步結果，不會產生多層的Callback結構。

## 資料來源

[使用 Promise][使用 Promise] @ MDN

[Promise 的使用][Promise 的使用] @ pjchender.dev


[使用 Promise]: https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Using_promises
[Promise 的使用]: https://pjchender.dev/javascript/js-promise/

<script>
window.tooltips = window.tooltips || []
window.tooltips.push(['#someId', { content: "This is the text of the tooltip!" }])
window.tooltips.push(['#someOtherId', { content: "{% include tooltips/example.html %}", placement: "right" }])
</script>
