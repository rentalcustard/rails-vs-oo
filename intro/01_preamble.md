!SLIDE bullets
# Rails vs object-oriented design #

!SLIDE bullets incremental
# About me #

* @mortice
* Not the other Tom Stuart!
* (OO) development - 4 years
* Ruby/Rails dev - 2 years

!SLIDE smallest
# Recent experience #
    +----------------------+-------+-------+---------+---------+-----+-------+
    | Name                 | Lines |   LOC | Classes | Methods | M/C | LOC/M |
    +----------------------+-------+-------+---------+---------+-----+-------+
    | Controllers          | 14551 | 10450 |     113 |    1127 |   9 |     7 |
    | Helpers              |  2832 |  2108 |       0 |     235 |   0 |     6 |
    | Models               | 21418 | 16315 |     341 |    1742 |   5 |     7 |
    | Libraries            |  9900 |  8807 |      41 |     311 |   7 |    26 |
    | APIs                 |   144 |   107 |       7 |       2 |   0 |    51 |
    | Functional tests     | 40158 | 32061 |     112 |    2808 |  25 |     9 |
    | Unit tests           | 19807 | 15513 |     113 |    1879 |  16 |     6 |
    | Model specs          | 25809 | 20253 |       3 |      26 |   8 |   776 |
    | View specs           | 10009 |  7962 |       2 |       7 |   3 |  1135 |
    | Controller specs     | 17697 | 13923 |       2 |      48 |  24 |   288 |
    | Helper specs         |  2630 |  2090 |       4 |       9 |   2 |   230 |
    | Library specs        |  2591 |  2034 |       6 |      25 |   4 |    79 |
    +----------------------+-------+-------+---------+---------+-----+-------+
    | Total                | 167546 | 131623 |     744 |    8219 |  11 |    14 |
    +----------------------+-------+-------+---------+---------+-----+-------+
      Code LOC: 37787     Test LOC: 93836     Code to Test Ratio: 1:2.5


<div id="player" style="display:none"></div>
<script>
    //Load player api asynchronously.
    var tag = document.createElement('script');
    tag.src = "http://www.youtube.com/player_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
    var done = false;
    var player;
    function onYouTubePlayerAPIReady() {
        player = new YT.Player('player', {
          height: '390',
          width: '640',
          videoId: 'WWaLxFIVX1s'
        });
    }

    window.onkeypress = function(e) {
      if (e.keyCode === 98) {
        player.playVideo();
      }
    };
</script>

!SLIDE bullets
# About this presentation

* Some ranting
* Mostly practical examples
* Just stuff I'm trying...

!SLIDE
# Massive thank you #

!SLIDE
# DISCLAIMER #
