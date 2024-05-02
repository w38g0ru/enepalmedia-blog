---
layout: post
title:  "सास (SASS)"
date:   2018-12-29 19:03:12 +0545
categories: tools
---

<img alt="सास (SASS)" border="0" data-original-height="320" data-original-width="320" height="200" src="https://2.bp.blogspot.com/-FZ2yFatTrMg/XCedvMI3ZJI/AAAAAAAAFrc/Coum1L1yPNMft0nAUWyiP8G4rb3_GCCAwCLcBGAs/s200/sass.png" title="सास (SASS) लोगो" width="200" />
<a href="https://sass-lang.com/" target="_blank">सास (SASS)</a> एक <a href="https://en.wikipedia.org/wiki/Cascading_Style_Sheets" target="_blank">सिएसएस (CSS)</a> एक्सटेन्सन हो जसले सिएसएस (CSS) लाई पनि एक प्रोग्रामिङ्ग ल्याङ्गवेजको जस्तो काम गराउछ ।&nbsp; सासको साहायताले सिसएसएस स्यान्टेक्सहरुले लेख्दा त्यसमा भेरिएबल , नेस्टेड रुल , मिनिङ्ग, ईनलाईन ईम्पोर्ट आदीको प्रयोग गर्न सकिन्छ ।<br />
<br />
उदारणको लागी तपाई एउटा सिएसए फाईल तयार गर्दै हुनुहुन्छ र फन्ट फेमिलि हरु बिभिन्न क्लास , ईलेमेन्टहरुमा प्रयोग गर्दा एकरुपता अपनाउन जरुरी छ भने त्यसलाई भेरीएबलको रुपमा सेभ गर्न सक्नु हुन्छ । र जहाँ जुन जुन सेलेक्टर , ईलेमेन्टमा सो फन्टको आवश्यकता पर्दछ त्यहाँ त्यो फन्ट भेरिएबल प्रयोग गर्न सक्नु हुन्छ ।&nbsp; ट्रेडिशनल सिएसएस मा यो सम्भव छैन त्यसैले सास को प्रयोग गरेर यस्तो गर्न सकिन्छ ।<br />
<!--more--><br />
<pre>$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
</pre>
सास को प्रयोग गरेर यस्तो सिएसएस बनाउन सकिन्छ । 
<br />
<pre>body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
</pre>
यो त सिएसएस कोड लेख्नको लागी सास मा भेरिएबलको प्रयोग मात्र भयो । सास मा सिएसएस फाईल तयार गर्नको लागी नेष्टेड रुल , मिनिग्स, ईनलाईन ईम्पोर्ट आदीको प्रयोग गर्न सकिन्छ । अब आऊनुस यिनिहरुको बारेमा छोटो चर्चा गरौ । <br />
<br />
<h3>
नेष्टेड रुल</h3>
सास को साहायताले एक अर्कामा अन्तर्निहित प्रपटिजहरु शेयर गर्न सक्दछन । उदारणको लागी
<br />
<pre>nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
</pre>
लेखेर त्यसलाई सिएसएस फाईलमा कम्पाईल गर्नु भो भने तल दिएको जस्तो सिएसएस स्यान्टेक्स तयार हुन्छ । 
<br />
<pre>nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
</pre>
<h3>
ईम्पोर्ट</h3>
सास को अर्को राम्रो र पक्ष भनेको टुक्रा टुक्रा कोडहरुलाई ईम्पोर्ट गरी एकै ठाँउमा सँग्रह गर्नु सक्न पनि हो । उदारणको लागि यती तपाईले कोडहरुलाई मेन्टेन गर्न सजिलो होस भने सानो सानो टुक्रा पारेर भिन्दा भिन्दै फाईलमा राख्नु भएको छ र त्यसलाई एकै पटक प्रयोग गर्न तल दिए अनुसार गर्न सकिन्छ । <br />
<pre>// _reset.scss

html,
body,
ul,
ol {
  margin:  0;
  padding: 0;
}

// base.scss

@import 'reset';

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;}

</pre>
माथीको उदारणमा एउटा रिसेट भन्ने फाईल छ त्यसमा सिएसएस रिसेटभ्यालहरु राखीएको छ र अर्को बेस भन्ने फाईलमा ईम्पोर्ट गर्ने हो भने सास को मद्दतले तल दिए अनुसारको सिएसएस फाईल बनाउन सकिन्छ । <br />
<pre>html,
body,
ul,
ol {
  margin:  0;
  padding: 0;
}

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
</pre>
<h3>
मिक्सीन</h3>
पिएचपी , जाभास्क्रीप्टका  फङ्गसन हरुमा जस्तो सास फाईलमा पनि भेरिएबल हरु आवश्यकता अनुसार पास गर्न सकिन्छ । <br />
<pre>@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.box { @include transform(rotate(30deg)); }
</pre>
सासमा मिक्सीनको प्रयोग गर्दा कुनै क्लासको नामको अगाडी @mixin लेख्न पर्छ । <br />
<pre>.box {
  -webkit-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  transform: rotate(30deg);
}
</pre>
<h3>
एक्सटेन्ड्स/ईनहेरिटेन्डस</h3>
यो सासको अर्को उपयोगी फिचर हो । यसमा सिएसएस प्रपर्टिजहरु एकबाट अर्को सेलेक्टरमा शेयरिङ्ग गरिन्छ । 
<br />
<pre>/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
</pre>
माथीको उदारणमा शेयर गरीएका सिएसएस प्रर्पटिजहरु तल दिए अनुसारका सेलेक्टरहरुमा यसरी शेयर गरिन्छ । 
<br />
<pre>/* This CSS will print because %message-shared is extended. */
.message, .success, .error, .warning {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}

</pre>
<h3>
अपरेटर</h3>
सिएसए फ्रेमवर्कहरुमा पाईन ग्रिड फिचरहरु यस्तै सास जस्तो प्रोग्रामको अपरेटर फिचर प्रयोग गरेर तयार गरिएको हुनु पर्छ ।
<br />
<pre>.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
</pre>
</div>
अब माथी दिइको कोडलाई सिएसएस फाईलमा कम्पाईल गर्दा यस्तो बन्छ । 
<br />
<pre>.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 62.5%;
}

aside[role="complementary"] {
  float: right;
  width: 31.25%;
}
</pre>
<h3>
सास (SASS) कसरी ईन्सटल गर्ने ?</h3>
माथीको उदारण पढेर यती तपाईलाई सास उपयोगी लाग्यो भने तपाई आफ्नो आवश्यकता अनुसार सासको सहयोगले सिएसएस फाईलहरु बनाउन सक्नु हुन्छ ।  विन्डोज मेसिनमा सास ईन्सटल गर्नको लागि सबै भन्दा पहिले नोड जेएस ईन्सटल गर्नु पर्छ । <a href="https://www.enepal.com.np/2018/12/how-to-install-nmp.html">यस भन्द अगाडीको पोष्टमा मैल नोड जेएस कसरि ईन्सटल गर्ने भन्ने उल्लेख गरेको छु</a> । अब नोडजेस ईन्सटल गरी सकेको भए सास ईन्सटल गर्नको लागी तल दिए अनुसार गर्न सकिन्छ । 
<br />
<pre>npm install -g sass
</pre>
अब माथी दिएको कुनै पनि उदारण लाई कपी गरेर .scss एक्सटेन्समा फाईल सेभ गर्नु होला । तपाईले फाईल कुन लोकेशनमा राख्नु भएको छ अनि कुन लोकेशनमा सिएसएस फाईल सेभ गर्ने हो याद गर्नु होला । अब माथी उल्लेख गरे अनुसारको सास फाईललाई सिएसए फाईल बनाउन तल दिएको कमाण्ड प्रयोग गर्नु होला । <br />
<pre>sass input.scss output.css
</pre>
मेरो उदारणको केसमा मैले जुन लोकेशनमा बसेर काम गरी गरी रहेको थिए त्यही लोकेशनमा सास फाईल सेभ गरे अनि त्यही लोकेशनमा सिएसएस फाईल क्रियट गरेको हुँ । 
