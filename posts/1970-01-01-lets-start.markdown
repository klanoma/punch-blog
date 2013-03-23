---
title: Let's Start!
published: true
tags:
- Punch
- Blog
- Life
---

It seems like there is a plethora of examples of interactive maps of the United States, but the internet is, rather unsurprisingly, lacking in the area of maps of our great white neighbors to the north. So here is an example of how I created an interactive map of Canada using a handy little Javascript library called [Raphaël](http://raphaeljs.com/).

First, you actually need a map of Canada in SVG format. Wikipedia is a great source for free media. I found a very detailed SVG map of [Canada here](http://en.wikipedia.org/wiki/File:Canada_blank_map.svg).

Next, you need to convert the SVG file into a javascript object that can be added to the Raphaël paper. There are a few decent conversion tools for this. The one that worked for me is [Ready Set Raphaël](http://readysetraphael.com/) Simply, upload the file, click “Check It”, and copy the resulting Javascript code. Your results may very depending on how cleanly the SVG was defined. In the case of the wikipedia file, the results are fantastic, but having had to use a specific designer’s file for my work, I had to spend quite a bit of time cleaning up the resulting code. Just be patient and remember that you may have to remove a significant number of paths in an effort to simplify the script. As you are going through it, for your sanity, I recommend that you assign all of the paths to variables with meaningful names.

Now, you have completed the most difficult part. Next, include the Raphaël library, create place to draw the map, and draw the map.

```javascript
  <script src="/scripts/libs/raphael-2.1.0.min.js" type="text/javascript" charset="utf-8"></script>
  <script type="text/javascript" charset="utf-8">
    window.onload = function () {

      var paper = ScaleRaphael("paper", 1391, 1347);
      var canada = {};
      canada.yukon = paper.path("M 1160.4397,680.67529 C 1159.3729,679.972 1155.125,677.88101 1151,676.02864 C 1144.7017,673.20033 1122.9778,661.92409 1087.3258,642.97723 C 1075.9927,636.95442 1034.4743,611.15123 1003.75,591.03597 C 992.86937,583.91239 988,580.15615 988,578.88637 C 988,576.35528 991.08744,571.50566 994.31523,568.96668 C 1000.1153,564.40432 996.76651,561.46008 985.36663,561.09919 C 983.10797,561.02769 982.08516,560.43367 981.70274,558.9713 C 981.41096,557.85551 980.79598,557.04466 980.33611,557.16942 C 978.46515,557.677 975.06194,555.77051 974.4614,553.8784 C 973.98352,552.37273 976.35217,548.12521 983.77357,537.17955 C 997.53744,516.87952 1022.9824,479.1969 1042.641,450 C 1058.2985,426.74555 1078.5312,396.76326 1105.8545,356.32552 L 1118.1348,338.15104 L 1121.3174,339.24785 C 1127.8773,341.50858 1129.7757,343.75969 1130.5183,350.15805 C 1130.8953,353.40604 1132.2542,358.13839 1133.5381,360.67437 C 1134.822,363.21036 1136.1654,367.01967 1136.5236,369.13949 C 1137.002,371.97103 1138.2569,373.92005 1141.2533,376.4848 C 1144.9739,379.66949 1145.2006,380.13052 1143.8366,381.73794 C 1141.7369,384.21243 1131.6192,400.69132 1129.2473,405.5 C 1128.1621,407.7 1126.4753,411.975 1125.4988,415 C 1124.5224,418.025 1122.7189,422.525 1121.4912,425 C 1117.1303,433.79134 1116.8821,433.12209 1127.4504,441.06576 C 1134.7288,446.53657 1137,448.79765 1137,450.57292 C 1137,451.854 1135.3903,455.98373 1133.4229,459.7501 C 1131.0878,464.22052 1129.6645,468.5098 1129.3234,472.10443 C 1128.8115,477.49997 1128.8743,477.66674 1132.4442,480.38965 C 1136.3423,483.36287 1136.1852,482.53687 1135.0646,494.17054 C 1135.0291,494.53934 1133.6831,495.13033 1132.0735,495.48385 C 1128.9088,496.17894 1126,499.73446 1126,502.90766 C 1126,503.99557 1125.0894,506.42911 1123.9763,508.31552 C 1121.7941,512.01414 1122.277,515.32518 1125.3736,517.89508 C 1126.514,518.84154 1126.8165,520.3141 1126.4575,523.17123 C 1126.0755,526.2119 1126.4783,527.86303 1128.188,530.26409 C 1129.784,532.50536 1130.4572,534.9735 1130.5598,538.95951 C 1130.639,542.03376 1131.4867,546.04055 1132.4535,547.91009 C 1134.137,551.1657 1134.1259,551.56578 1132.1614,558.39741 C 1129.5496,567.47989 1128.2794,574.5708 1127.5476,584.15358 C 1127.2262,588.36305 1126.4667,593.2313 1125.86,594.9719 C 1124.8791,597.7856 1125.034,598.43409 1127.2562,600.81832 C 1130.5945,604.40005 1131.5264,606.3735 1133.4917,614.02337 C 1134.4068,617.58552 1136.4131,622.83639 1137.9501,625.69198 C 1139.991,629.48351 1140.4019,631.01553 1139.4736,631.37174 C 1138.7745,631.64002 1137.9749,634.02863 1137.6968,636.67976 C 1137.4186,639.33089 1136.8665,642.75902 1136.4698,644.29783 C 1135.61,647.63328 1136.8878,648.87411 1145,652.5813 C 1148.025,653.96368 1152.2306,656.28946 1154.3457,657.74969 C 1156.4608,659.20992 1159.3858,660.4261 1160.8457,660.45233 L 1163.5,660.5 L 1163.221,670.94563 C 1163.0676,676.69072 1162.8155,681.51787 1162.6607,681.67263 C 1162.506,681.82738 1161.5065,681.37858 1160.4397,680.67529 z ").attr({fill: "#522405","stroke-width": 0}).transform("t-959.79,0.708441");

    };
  </script>

  <div id="paper"></div>
```

Stay tuned for [Part 2: Adding tool tips to the javascript interactive map of Canada](#)

[See the full demo with the code.](http://demos.williamyoumans.com/canada-interactive-map.php)