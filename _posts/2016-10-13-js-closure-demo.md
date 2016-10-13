---
layout: post
title: js-closure-demo
---
#### js closure demo

```
<div id="js-venue-book-venues" class="venue-list">
        {{each venues}}
            {{if $value.venue}}
            <div class="card">
                <a id="js-venuebook-venues-{{$index}}" venue-name="{{$value.venue.name}}" venue-id="{{$value.venue.id}}" href="javascript:void(0)" target="_self">

                ...

                </a>

                {{if $value.explanation}}
                <div class="introduce">
                    <div class="col-left">
                        <div class="white-line">
                            <hr>
                        </div>
                    </div>
                    <div class="col-right">
                        <div class="text">{{#$value.explanation}}</div>
                    </div>
                </div>
                {{/if}}
            </div>
            {{/if}}
        {{/each}}
    </div>
    ```
    ```
    function goToVenuePage(i) {

        var venueName = document.getElementById('js-venuebook-venues-' + i).getAttribute("venue-name");
        var venueId = document.getElementById('js-venuebook-venues-' + i).getAttribute("venue-id");

        if (venueName && i) {

            userEvent.baidu_stats.venuebook_venueCard.push(venueName);
            userEvent.baidu_stats.venuebook_venueCard.push(i);

            userEvent.google_stats.venuebook_venueCard.eventLabel = venueName;
            userEvent.google_stats.venuebook_venueCard.eventValue = i;
        }

        //百度统计
        if (_hmt) _hmt.push(userEvent.baidu_stats.venuebook_venueCard);
        //谷歌统计
        if (ga) ga('send', userEvent.google_stats.venuebook_venueCard);

        window.location.href = "/venue/" + venueId;
    }

    function renderVenueListContent() {

      ...
      // render content
      renderTemplate('js-list-container-template', 'js-venue-list-container', __CONST.venuebook);

      function venueCardClick(i) {

          return function () {
              goToVenuePage(i);
          }
      }

      if (venues && venues.length) {
          for (var i = 0; i < venues.length; i++) {
              document.getElementById('js-venuebook-venues-' + i).addEventListener('click', venueCardClick(i), false);
          }
      }
  }
    ````
