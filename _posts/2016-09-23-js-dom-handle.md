---
layout: post
title: js-dom-handle
---
#### use superagent

```
document.getElementById('js-like-button').addEventListener('click', venueLike, false);
document.getElementById('js-been-button').addEventListener('click', venueBeen, false);
document.addEventListener('DOMContentLoaded', init, false);
```

```
/**
 * [地点去过]
 */
function toggleBeenVenue() {

    if (__CONST.venueProfile.haveBeen) {

        request
            .post('/api/venue/' + __CONST.venueProfile.id + '/cancelBeenVenue')
            .set('Accept', 'application/json')
            .end(function (err, res) {
                if (err) {
                    // 处理未登录的情况
                    if (res.body.code === 20000) {
                        window.location.href = '/wechat-login?returnURL=' + encodeURIComponent(window.location.href);
                        return;
                    }

                    console.log("ajax调用出现异常:" + err);
                    return;
                }

                __CONST.venueProfile.haveBeen = false;
                __CONST.venueProfile.beenPeopleCount -=1;

                document.getElementById("js-been-button").classList.add("have-been");
                document.getElementById("js-been-venue-icons").className = "icons-venue small icon-flag";
                document.getElementById("beenPeopleCountVenue").innerText = __CONST.venueProfile.beenPeopleCount.toString();

            });
    } else {
        request
            .post('/api/venue/' + __CONST.venueProfile.id + '/setBeenVenue')
            .set('Accept', 'application/json')
            .end(function (err, res) {
                if (err) {
                    // 处理未登录的情况
                    if (res.body.code === 20000) {
                        window.location.href = '/wechat-login?returnURL=' + encodeURIComponent(window.location.href);
                        return;
                    }

                    console.log("ajax调用出现异常:" + err);
                    return;
                }

                __CONST.venueProfile.haveBeen = true;
                __CONST.venueProfile.beenPeopleCount += 1;

                document.getElementById("js-been-button").classList.remove("have-been");
                document.getElementById("js-been-venue-icons").className = "icons-venue small icon-check";
                document.getElementById("beenPeopleCountVenue").innerText = __CONST.venueProfile.beenPeopleCount.toString();

            });
    }
}

/**
 * 点击评论，跳转到App Store的下载页面，如果本机安装了App，则打开App对应的地点集页面
 */
function openAppAndGotoAppStore() {
    var venueId = location.pathname.substring(location.pathname.lastIndexOf('/') + 1);
    window.location.href = config.iosAppUrlPrefix + "venue/" + venueId;

    setTimeout(function () {
        window.location.href = config.appStore;
    }, 250);
}


```
