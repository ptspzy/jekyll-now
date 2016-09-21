---
layout: post
title: js-dom-handle
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.

```
document.getElementById('js-like-button').addEventListener('click', venueLike, false);
document.getElementById('js-been-button').addEventListener('click', venueBeen, false);
```

```

document.addEventListener('DOMContentLoaded', init, false);


/**
 * [地点收藏]
 */
function venueLike() {

    var isLike = false;
    var venueId = '1000386';

    if (!isLike) {
        request
            .post('/api/venue/' + venueId + '/like')
            .set('Accept', 'application/json')
            .end(function (err, res) {
                if (err || !res.ok) {
                    alert('Oh no! error');
                } else {
                    alert('yay got ' + JSON.stringify(res.body));
                    document.getElementById("js-like-button").className = "icons-venue small icon-collected";

                }
            });
    } else {
        request
            .post('/api/venue/' + venueId + '/unlike')
            .set('Accept', 'application/json')
            .end(function (err, res) {
                if (err || !res.ok) {
                    alert('Oh no! error');
                } else {
                    alert('yay got ' + JSON.stringify(res.body));
                    document.getElementById("js-like-button").className = "icons-venue small icon-collect";
                }
            });
    }

}

/**
 * [地点去过]
 */
function venueBeen() {

    var venueId = '1000386';

    if (! __CONST.venueProfile.haveBeen) {
        request
            .post('/api/venue/' + venueId + '/setBeenVenue')
            .set('Accept', 'application/json')
            .end(function (err, res) {
                if (err || !res.ok) {
                    alert('Oh no! error');
                } else {
                    alert('yay got ' + JSON.stringify(res.body));
                    __CONST.venueProfile.haveBeen = true;
                    document.getElementById("js-been-button").className = "button-container have-been";
                    document.getElementById("js-been-button").firstElementChild.className = "icons-venue small icon-check";
                }
            });
    } else {
        request
            .post('/api/venue/' + venueId + '/cancelBeenVenue')
            .set('Accept', 'application/json')
            .end(function (err, res) {
                if (err || !res.ok) {
                    alert('Oh no! error');
                } else {
                    alert('yay got ' + JSON.stringify(res.body));
                    __CONST.venueProfile.haveBeen = false;
                    document.getElementById("js-been-button").className = "button-container";
                    document.getElementById("js-been-button").firstElementChild.className = "icons-venue small icon-flag";
                }
            });
    }
}

```
