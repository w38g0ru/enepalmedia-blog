---
layout: post
title:  "पाइथन प्लटी एक्सप्रेसमा प्रयोग हुने ग्राफका प्रकार"
date:   2025-01-17 20:38:12 +0545
---
<a href="https://plotly.com/python/plotly-express/" target="_blank"> पाइथन प्लटी एक्सप्रेस </a> मा विभिन्न ग्राफहरू जस्तै स्क्याटर प्लट, लाइन प्लट, बार चार्ट, हिस्टोग्राम, बक्स प्लट, डेनसिटी हीटम्याप, र पाई चार्ट प्रयोग गरेर दुई वा बढी भेरिएबलहरूको सम्बन्ध, समयसँगको परिवर्तन, क्याटेगोरिकल डाटाको तुलना, वितरण, र अनुपातको विश्लेषण गर्न सकिन्छ। उदाहरणका रूपमा, दिउसो न्युरोड गल्लीमा हुने व्यापारलाई अनुमान गर्न, तापमान र ग्राहक खर्चका बीचको सम्बन्धलाई स्क्याटर प्लटमा देखाउन सकिन्छ, दिनको समयमा ग्राहक खर्चको परिवर्तनलाई लाइन प्लटमा देखाउन सकिन्छ, र विभिन्न समय अवधिमा भएका बिक्रीलाई बार चार्टमा तुलना गर्न सकिन्छ। यसरी, विभिन्न चार्टहरू प्रयोग गरेर व्यापारका डाटाको विश्लेषण गर्न सकिन्छ र भविष्यका ट्रेन्ड र व्यावसायिक निर्णयहरूमा मद्दत गर्न सकिन्छ।

# Scatter Plot
<audio controls>
  <source src="{{ '/audio/scatter-plot.mp3' | relative_url }}" type="audio/mp3">
  Your browser does not support the audio element.
</audio>
स्क्याटर प्लट भनेको एउटा ग्राफ हो जसले दुई वटा भेरिएबल बीचको सम्बन्ध देखाउँछ। यसमा एउटा भेरिएबललाई एक्स-एक्सिसमा र अर्को भेरिएबललाई वाई-एक्सिसमा राखिन्छ। यसले दुई भेरिएबलको बीचमा कस्तो प्रकारको सम्बन्ध छ भन्ने कुरा ग्राफको माध्यमबाट प्रष्ट पार्छ। साधारणतया, यस ग्राफको प्रयोग correlation, clusters, र trends देखाउनका लागि उपयुक्त हुन्छ। 

उदाहरणको लागि: मानौं, तपाईलाई सिजन अनुसार खरिद-बिक्रीको अध्ययन गर्नु छ। यदि तपाई तापक्रम अनुसार ग्राहकले कति खर्च गर्छन् भन्ने कुरा बुझ्न चाहनुहुन्छ भने, स्क्याटर प्लटको मद्दतले तपाईं यसलाई बुझ्न सक्नुहुन्छ। यसका लागि,  एक्स-एक्सिसमा तापक्रम राख्नुहोस् (अर्थात्, जति तातो, त्यति बढी अंक) र वाइ-एक्सिसमा सपिङ खर्च राख्नुहोस्। अब, स्क्याटर ग्राफको सहयोगले  तापमानसँगै खर्च बढिरहेको छ कि घटिरहेको छ थाहा पाउन सकिन्छ ।
अर्थात, यदि प्वाईन्टहरू माथि जान्छ भने, यसको अर्थ हो कि गर्मीको समयमा मानिसहरूले बढी खर्च गर्छन् । यदि प्वाईन्टहरू तल जान्छ भने, यसको अर्थ हो कि गर्मीको समयमा खर्च कम हुन्छ । यसरी, स्क्याटर प्लटले दुई भेरिएबल बीचको सम्बन्धलाई बुझ्नमा मद्दत गर्छ।

![Bar Image]({{ "/images/scatter.png" | relative_url }})

``` python

import plotly.express as px
import pandas as pd

# Create a sample dataset
data = {
    'Temperature': [20, 25, 30, 35, 40, 45, 50],
    'Shopping_Spending': [150, 200, 250, 300, 350, 400, 450]
}

# Convert to DataFrame
df = pd.DataFrame(data)

# Create a scatter plot
fig = px.scatter(df, x='Temperature', y='Shopping_Spending', title="Temperature vs Shopping Spending",
                 labels={'Temperature': 'Temperature (°C)', 'Shopping_Spending': 'Shopping Spending ($)'})

# Show the plot
fig.show()

```
# Line Plot
<audio controls>
  <source src="{{ '/audio/line.mp3' | relative_url }}" type="audio/mp3">
  Your browser does not support the audio element.
</audio>
लाइन प्लट भनेको एउटा ग्राफ हो जसले समयको क्रममा भएको परिवर्तनलाई देखाउँछ। यसमा समयलाई एक्स-एक्सिसमा र परिवर्तन हुने भेरिएबललाई वाई-एक्सिसमा राखिन्छ। यसले समयसँगै कुनै एक भेरिएबलको भ्यालुमा कस्तो परिवर्तन भइरहेको छ भन्ने कुरा ग्राफको माध्यमबाट प्रष्ट पार्दछ। साधारणतया, यस ग्राफको प्रयोग समय सँगै भएका ट्रेन्ड, परिवर्तन, र भविष्यको अनुमान गर्नका लागि उपयुक्त हुन्छ।

उदाहरणको लागि: मानौं, तपाईलाई कुनै एक दिनभरिमा कुन समयामा ग्राहकले कति खरिद गर्छन् भन्ने कुरा बुझ्न छ भने, लाइन प्लटको मद्दतले तपाईं यसलाई अध्ययन गर्न सक्नुहुन्छ। यसका लागि, एक्स-एक्सिसमा समय (घण्टा) राख्नु पर्दछ र वाइ-एक्सिसमा बिक्री राख्नु पर्दछ।
अब, लाइन ग्राफको सहयोगले तपाईंलाई समय अनुसार कतिखेर धेरै बिक्री हुन्छ र कतिखेर कम हुन्छ भन्ने थाहा पाउन सकिन्छ । यहाँ यदि लाईन माथि जान्छ भने, यसको अर्थ हो कि दिन ढल्दै जाँदा किन्ने मानिसहरूले बढी आउछन र धेरै खरिद गर्छन् । यदि लाईन तल जान्छ भने, यसको अर्थ हो कि दिन ढल्दै जाँदा मान्छेहरू कम आउछन र कम बिक्रि हुन्छ।

यसरी, लाइन प्लटले समयसँग सम्बन्धित भेरिएबलको परिवर्तनलाई बुझ्नमा मद्दत गर्छ।

![Bar Image]({{ "/images/line.png" | relative_url }})

``` python
import plotly.express as px
import pandas as pd

# Create a sample dataset
data = {
    'Time': ['9 AM', '12 PM', '5 PM'],
    'Shopping_Spending': [100, 200, 150]
}

# Convert to DataFrame
df = pd.DataFrame(data)

# Create a line plot
fig = px.line(df, x='Time', y='Shopping_Spending', title="Shopping Spending Throughout the Day",
              labels={'Shopping_Spending': 'Shopping Spending ($)', 'Time': 'Time of Day'})

# Show the plot
fig.show()

```
# Bar Chart
<audio controls>
  <source src="{{ '/audio/bar.mp3' | relative_url }}" type="audio/mp3">
  Your browser does not support the audio element.
</audio>
बार चार्ट क्याटेगोरिकल डाटा को तुलना गर्न प्रयोग गरिन्छ। यसमा विभिन्न क्याटेगोरीहरूको तुलना गर्नका लागि बारहरूको उचाई लाई आधार मानी जानकारी प्रस्तुत गरिन्छ। यसले बारको हाइटको आधारमा तुलना गर्न सहयोग गर्दछ ।

उदाहरणको लागि, मानौं तपाईंलाई दिन भरी निश्चीत समयवधीको आधारमा कति बिक्री भएको छ भन्ने कुरा जान्न छ भने, तपाईं बार चार्टको प्रयोग गर्न सक्नुहुन्छ। यसका लागि, तपाईंको एक्स-एक्सिसमा समयको क्याटेगोरी राख्नु पर्दछ , जस्तै १० देखी १ बजे, १ देखी ४ बजे, र ४ देखी ७ बजे। वाइ-एक्सिसमा त्यस समयमा भएको बिक्रीको रकम राख्नु पर्दछ । त्यसपछी तुलनात्मक रुपमा कुन समयमा धेरै बिक्रि हुन्छ र कुन समयमा कम बिक्री हुन्छ ग्राफ हेरेर नै थाहा पाउन सकिन्छ । 

![Bar Image]({{ "/images/bar.png" | relative_url }})

``` python
import plotly.express as px
import pandas as pd

# Create a sample dataset for sales in different time periods
data = {
    'Time_Period': ['10 AM - 1 PM', '1 PM - 4 PM', '4 PM - 7 PM'],
    'Sales': [500, 1000, 750]
}

# Convert to DataFrame
df = pd.DataFrame(data)

# Create a bar chart
fig = px.bar(df, x='Time_Period', y='Sales', title="Sales by Time Period",
             labels={'Sales': 'Sales ($)', 'Time_Period': 'Time Period'})

# Show the plot
fig.show()

```
# Histogram
<audio controls>
  <source src="{{ '/audio/histogram.mp3' | relative_url }}" type="audio/mp3">
  Your browser does not support the audio element.
</audio>
सिंगल न्युमेरिकल भेरीएबलको डिस्ट्रीब्युसन देखाउन हिस्टोग्रामको प्रयोग गर्न सकिन्छ। हिस्टोग्राम ग्राफ बनाउनका लागि एउटा मात्र संख्यात्मक डाटा (जस्तै, ग्राहकहरूको खरिद रकम) लिइन्छ र त्यस डाटाको वितरण विश्लेषण गर्न हिस्टोग्राम चार्ट प्रयोग गरिन्छ। हिस्टोग्राम चार्टले डाटा कुन रेंजमा कति धेरै वा कम छ भनेर विश्लेषण गर्दछ। यसमा, डाटा निश्चित अन्तराल (bins) मा वर्गीकृत गरिन्छ र प्रत्येक बिनको लागि एउटा बार हुन्छ जसले त्यस बिनको भित्रको डाटा कति छ भनेर देखाउँछ।

उदाहरणको लागि, तपाईंको सँग १०० ग्राहकहरूको खरिद रकमको डाटा छ। तपाईं यो डाटाको माध्यमबाट कति ग्राहकले कति देखि कति सम्म पैसा खर्च गरेका छन् भन्ने कुरा ग्राफिकल रूपमा व्यक्त गर्न सक्नुहुन्छ। त्यसका लागि तपाईं हिस्टोग्राम चार्टको प्रयोग गर्नु पर्दछ।

![Bar Image]({{ "/images/histogram.png" | relative_url }})

``` python
import plotly.express as px

# Data for customer spending
data = {
    'Spending Range': ['0-50', '50-100', '100-150', '150-200'],
    'Number of Customers': [30, 50, 10, 5]
}

# Create a histogram using Plotly Express
fig = px.bar(data, x='Spending Range', y='Number of Customers', title="Customer Spending Distribution",
             labels={'Spending Range': 'Spending Range (in dollars)', 'Number of Customers': 'Number of Customers'})

# Show the plot
fig.show()

```
# Box Plot
<audio controls>
  <source src="{{ '/audio/box.mp3' | relative_url }}" type="audio/mp3">
  Your browser does not support the audio element.
</audio>
बक्स प्लट भनेको एक प्रकारको ग्राफ हो जसले डाटाको Distribution, Median, Spread or Dispersion, र विभिन्न क्वार्टाइलहरूको (क्वार्टाइल १, मिडियन, क्वार्टाइल ३) विश्लेषण गर्न मद्दत गर्छ। यो ग्राफले डाटा सेटको बारेमा महत्वपूर्ण जानकारीको सारांश दिन्छ।

उदाहरणको रूपमा, हामी माथि दिइएको ग्राहकहरूको खरिद रकमको डाटालाई बक्स प्लटको मद्दतले विश्लेषण गर्न सक्छौं। बक्स प्लटले डाटाको मध्य मान, न्यूनतम र अधिकतम मान, र २५ प्रतिशत र ७५ प्रतिशतका क्वार्टाइलहरू देखाउँछ।

हामीसँग १०० ग्राहकहरूको खरिद रकमको डाटा छ, जसलाई विभिन्न श्रेणीहरूमा विभाजित गर्न सकिन्छ, जस्तै ०-५० रुपयाँ, ५०-१००  रुपयाँ, १००-१५०  रुपयाँ, र १५०-२००  रुपयाँ । बक्स प्लटको माध्यमबाट हामी प्रत्येक श्रेणीको डाटा Distribution लाई देख्न सक्छौं।

![Bar Image]({{ "/images/box.png" | relative_url }})

``` python
import plotly.express as px
import pandas as pd

# Sample data for spending
spending_data = [50, 80, 90, 200, 30, 45, 100, 60, 120, 160, 50, 95, 180, 55, 130, 140, 75, 85, 110, 45]

# Create DataFrame
df = pd.DataFrame(spending_data, columns=['Spending'])

# Create the box plot using Plotly
fig = px.box(df, y="Spending", title="Customer Spending Distribution (Box Plot)",
             labels={'Spending': 'Spending (in dollars)'})

# Show the plot
fig.show()

```
# Density Heatmap
<audio controls>
  <source src="{{ '/audio/density.mp3' | relative_url }}" type="audio/mp3">
  Your browser does not support the audio element.
</audio>
Density heatmap एक प्रकारको ग्राफ हो जसले दुई भेरिएबलहरूको बीचमा डाटाको घनत्व देखाउँछ। यसमा, प्रत्येक पिक्सल (या सेल) को रंगको गहिराईले त्यहाँको डाटाको घनत्वलाई जनाउँछ। यसले तपाईलाई डाटा बिन्दुहरूको सघनता (density) बुझ्नमा मद्दत गर्छ।

माथि दिएको ग्राहक खर्च डाटा उदाहरणमा, हामी दुई भेरिएबलहरू, जस्तै खर्च र समयको आधारमा डाटाको घनत्व देखाउनका लागि density heatmap प्रयोग गर्न सक्छौं। मानौं, तपाईंको पास ग्राहकहरूको खर्च र विभिन्न समयमा गरिएको खरिदको डाटा छ। यसमा, तपाईं विभिन्न समयको अवधिमा ग्राहकहरूको खर्चमा हुने घनत्वको विश्लेषण गर्न सक्नुहुन्छ।

![Bar Image]({{ "/images/heatmap.png" | relative_url }})

``` python
import plotly.express as px
import pandas as pd

# ग्राहक खर्च र समयको कस्टम डाटा
data = {
    'Time': ['10-1 PM', '1-4 PM', '4-7 PM', '10-1 PM', '1-4 PM', '4-7 PM', '10-1 PM', '1-4 PM', '4-7 PM'],
    'Spending': [50, 200, 150, 30, 120, 180, 60, 90, 100]
}

# पाण्डास डाटाफ्रेम निर्माण
df = pd.DataFrame(data)

# Density Heatmap बनाउने
fig = px.density_heatmap(df, x="Time", y="Spending", title="Density Heatmap of Customer Spending by Time",
                         labels={'Time': 'समय', 'Spending': 'खर्च (डलरमा)'})

# ग्राफ देखाउने
fig.show()

```
# Pie Chart
Pie chart को प्रयोग प्रायः क्याटेगोरिकल डाटाको अनुपातको तुलनात्मक विश्लेषण गर्नका लागि गरिन्छ। यो चार्टले प्रत्येक क्याटेगोरीको अनुपातलाई एक गोलाकार चार्टको रुपमा देखाउँछ, जसको प्रत्येक खण्डले एक क्याटेगोरीको अंश देखाउँछ। तपाईंले विभिन्न क्याटेगोरीहरूका बीचको अनुपातलाई सहजै देख्न सक्छन्।

अब, हामी माथिको उदाहरणमा ग्राहक खर्च र समयको आधारमा Pie chart प्रयोग गरेर यसलाई व्याख्या गर्नेछौं। यसमा, हामी समयका ३ क्याटेगोरीहरूलाई (१०-१ बजे, १-४ बजे, र ४-७ बजे) Pie chart मा देखाउँछौं र हरेक समयको अवधिमा ग्राहकहरूको खर्चको अनुपात कस्तो छ भनेर देखाउँछौं।

![Bar Image]({{ "/images/pie.png" | relative_url }})

``` python
import plotly.express as px
import pandas as pd

# ग्राहक खर्च र समयको कस्टम डाटा
data = {
    'Time': ['10-1 PM', '1-4 PM', '4-7 PM', '10-1 PM', '1-4 PM', '4-7 PM', '10-1 PM', '1-4 PM', '4-7 PM'],
    'Spending': [50, 200, 150, 30, 120, 180, 60, 90, 100]
}

# पाण्डास डाटाफ्रेम निर्माण
df = pd.DataFrame(data)

# समयको अनुसार खर्चको कुल रकम गणना
time_spending = df.groupby('Time')['Spending'].sum().reset_index()

# Pie chart बनाउने
fig = px.pie(time_spending, names='Time', values='Spending', title="Pie Chart of Customer Spending by Time",
             labels={'Time': 'समय', 'Spending': 'खर्च (डलरमा)'})

# ग्राफ देखाउने
fig.show()

```
