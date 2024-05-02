---
layout: post
title:  "सिम्पल ग्रिड सिएसएस फ्रेमवर्क"
date:   2018-12-29 19:03:12 +0545
categories: tools
---

<img border="0" data-original-height="900" data-original-width="1200" height="240" src="https://4.bp.blogspot.com/-27z-vrf3-fo/XCehu62-_LI/AAAAAAAAFro/Hw2aRE7etp0TR6MA7jBczFjXWAdMOK8XACLcBGAs/s320/simple-grid-css.png" width="320" />
अघिल्ला ट्युटोरियलहरुमा <a href="https://www.enepal.com.np/2018/12/how-to-install-nmp.html" target="_blank">नोड जेस ईन्सटल</a> गरी <a href="https://www.enepal.com.np/2018/12/conditional-css.html" target="_blank">सास चलाई सक्नु भएको </a>भए यो फ्रेमवर्क बुझ्न तपाईलाई सजिलो हुन्छ । यस सिएसएस फ्रेमवर्कमा तपाई आफै केही प्रपर्टिजहरु थप्न वा भएकालाई परिमार्जन पनि गर्न सक्नु हुन्छ ।<br />
<br />
त्यो भन्दा पहिले <a href="https://simplegrid.io/" target="_blank">सिम्पल ग्रिड सिएसएस (Simple Grid CSS)</a> बारे केही जानकारी लिउँ । यो स्क्रीनलाई १२ भागमा बिभाजन गरेर जुन सुकै डिभाईसमा पनि फिट हुने गरी बनाईएको एउटा छरितो (फाईल साईज र यसको बिशेशताको आधारमा) खालको सिएसएस फ्रेमवर्क हो । बुटस्ट्राप जस्तै यस सिएसएस मा पनि कन्टेनर भित्र रो अनि रो भित्र कोलमहरु हुन सक्छन । कन्टेनरको साईज ९६० पिक्सेल रहेको छ । यसलाई आवश्यकता अनुसार थपघट गर्न सकिन्छ । यस सिएसएसमा टाईपोग्राफी भन्दा पनि ग्रिड सिस्टमलाई महत्व दिएको छ । त्यसैले ग्रिडमा आधारित ग्रिड लेआउट बनाउन यो उपयोगी देखीन्छ ।<br />
<br />
<!--more--><br />
<br />
अब यस फ्रेमवर्क र सासको बारेमा बुझ्नको लागी <a href="https://simplegrid.io/" target="_blank">यस फ्रेमवर्कको अफिसियल वेबसाईट</a> वा <a href="https://github.com/zachacole/Simple-Grid" target="_blank">गिटहब बाट यसलाई डाउनलोड गरौ</a> । यस फ्रेमवर्कलाई तपाईले आफ्नो कम्प्युटरमा डाउनलोड गरी सके पछी सयको जिप फाईल अनजिप गरेर हेर्नु भो भने त्यहाँ .scss एक्सटेन्सन भएको फाईल भेट्नु हुन्छ । अब त्यसलाई खोलेर हेर्नु भो भने तल दिए अनुसारको स्यानटेक्सहरु भेट्नु हुन्छ ।<br />
<br />
<pre>/ SIMPLE GRID - SASS/SCSS

@import url(https://fonts.googleapis.com/css?family=Lato:400,300,300italic,400italic,700,700italic);

<mark>
// fonts
$font-family: 'Lato', Helvetica, sans-serif;
$font-weight-light: 300;
$font-weight-regular: 400;
$font-weight-heavy: 700;
$font-height: 1.5;


// colors
$dark-grey: #333447;
$dark-gray: #333447; // for the Americans
</mark>
// universal

html,
body {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
  left: 0;
  top: 0;
  font-size: 100%;
}

* {
  font-family: $font-family;
  color: $dark-grey;
  line-height: $font-height;
}

// typography

h1 {
  font-size: 2.5rem;
}

h2 {
  font-size: 2rem;
}

h3 {
  font-size: 1.375rem;
}

h4 {
  font-size: 1.125rem;
}

h5 {
  font-size: 1rem;
}

h6 {
  font-size: 0.875rem;
}

p {
  font-size: 1.125rem;
  font-weight: 200;
  line-height: 1.8;
}

.font-light {
  font-weight: $font-weight-light;
}

.font-regular {
  font-weight: $font-weight-regular;
}

.font-heavy {
  font-weight: $font-weight-heavy;
}

// utility

.left {
  text-align: left;
}

.right {
  text-align: right;
}

.center {
  text-align: center;
  margin-left: auto;
  margin-right: auto;
}

.justify {
  text-align: justify;
}

.hidden-sm {
  display: none;
}
<mark>
// grid

$width: 96%;
$gutter: 4%;
$breakpoint-small: 33.75em; // 540px
$breakpoint-med: 45em; // 720px
$breakpoint-large: 60em; // 960px
</mark>
.container {
  width: 90%;
  margin-left: auto;
  margin-right: auto;

  @media only screen and (min-width: $breakpoint-small) {
    width: 80%;
  }

  @media only screen and (min-width: $breakpoint-large) {
    width: 75%;
    max-width: 60rem;
  }
}

.row {
  position: relative;
  width: 100%;
}

.row [class^="col"] {
  float: left;
  margin: 0.5rem 2%;
  min-height: 0.125rem;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

.col-1,
.col-2,
.col-3,
.col-4,
.col-5,
.col-6,
.col-7,
.col-8,
.col-9,
.col-10,
.col-11,
.col-12 {
  width: $width;
}

.col-1-sm { width:($width / 12) - ($gutter * 11 / 12); }
.col-2-sm { width: ($width / 6) - ($gutter * 10 / 12); }
.col-3-sm { width: ($width / 4) - ($gutter * 9 / 12); }
.col-4-sm { width: ($width / 3) - ($gutter * 8 / 12); }
.col-5-sm { width: ($width / (12 / 5)) - ($gutter * 7 / 12); }
.col-6-sm { width: ($width / 2) - ($gutter * 6 / 12); }
.col-7-sm { width: ($width / (12 / 7)) - ($gutter * 5 / 12); }
.col-8-sm { width: ($width / (12 / 8)) - ($gutter * 4 / 12); }
.col-9-sm { width: ($width / (12 / 9)) - ($gutter * 3 / 12); }
.col-10-sm { width: ($width / (12 / 10)) - ($gutter * 2 / 12); }
.col-11-sm { width: ($width / (12 / 11)) - ($gutter * 1 / 12); }
.col-12-sm { width: $width; }

@media only screen and (min-width: $breakpoint-med) {
  .col-1 { width:($width / 12) - ($gutter * 11 / 12); }
  .col-2 { width: ($width / 6) - ($gutter * 10 / 12); }
  .col-3 { width: ($width / 4) - ($gutter * 9 / 12); }
  .col-4 { width: ($width / 3) - ($gutter * 8 / 12); }
  .col-5 { width: ($width / (12 / 5)) - ($gutter * 7 / 12); }
  .col-6 { width: ($width / 2) - ($gutter * 6 / 12); }
  .col-7 { width: ($width / (12 / 7)) - ($gutter * 5 / 12); }
  .col-8 { width: ($width / (12 / 8)) - ($gutter * 4 / 12); }
  .col-9 { width: ($width / (12 / 9)) - ($gutter * 3 / 12); }
  .col-10 { width: ($width / (12 / 10)) - ($gutter * 2 / 12); }
  .col-11 { width: ($width / (12 / 11)) - ($gutter * 1 / 12); }
  .col-12 { width: $width; }

  .hidden-sm {
    display: block;
  }
}
</pre>
माथी हाईलाईट गरेको भेरीएबलहको भ्याल चेन्ज गरेर यस .scss फाईल लाई कम्पाईल गर्ने हो भने जहाँ जहाँ त्यो भेरिएबलहरु प्रयोग भएका छन त्यहाँ सबै ठाँउमा भ्यालुहरु चेन्ज हुन्छ । सास (SASS) को रमाईलो/उपयोगी कुरा नै यही हो । 

मेरो पछिल्लो ब्लग फलो गर्दा पनि कसरी गर्ने भन्ने झुक्कीनु भो भने कमेन्ट गर्नु होला । म प्रस्ट्याउने प्रया गर्ने छु । 

