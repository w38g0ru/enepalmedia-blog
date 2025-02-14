---
layout: post
title: "पाईथन लाईब्रेरी पान्डास ट्युटोरियल "
date: 2025-02-12 08:44:12 +0545
---

# 📌 pandas को आधारभूत ट्यूटोरियल (सप्ताह १-२) – नेपालीमा  
🚀 **pandas** एक शक्तिशाली **Python लाइब्रेरी** हो, जसले डाटा विश्लेषण (Data Analysis) र हेरफेर (Data Manipulation) गर्न मद्दत गर्छ।  

## १. pandas इन्स्टल गर्ने र सेटअप गर्ने  
```python
pip install pandas
import pandas as pd
```

## २. pandas को मुख्य डाटा संरचना (Data Structures)  
### 🟢 Series बनाउने तरिका  
```python
import pandas as pd

data = [10, 20, 30, 40]
series = pd.Series(data)
print(series)
```

### 🟢 DataFrame बनाउने तरिका  
```python
data = {
    "नाम": ["राम", "सीता", "गिता"],
    "उमेर": [25, 22, 28],
    "शहर": ["काठमाडौं", "पोखरा", "ललितपुर"]
}
df = pd.DataFrame(data)
print(df)
```

## ३. DataFrame को आधारभूत अपरेशनहरू  
```python
print(df.head())  # पहिलो ५ पंक्ति
print(df.dtypes)  # डाटा प्रकार
```

## ४. DataFrame बाट डाटा चयन (Selection)  
```python
print(df["नाम"])  # विशेष स्तम्भ चयन
print(df.loc[1])   # विशेष पंक्ति चयन
```

## ५. फिल्टरिंग (Filtering) – कन्डिसनल सिलेक्शन  
```python
print(df[df["उमेर"] > 25])
```

## 🎯 अभ्यास (Exercises)  
- **Q1:** ५ जनाको नाम, उमेर र शहर भएको DataFrame बनाउनुहोस्।  
- **Q2:** ३० भन्दा कम उमेर भएका व्यक्तिहरू छान्नुहोस्।  
- **Q3:** नयाँ स्तम्भ "पेशा" थप्नुहोस्।  

🎉 **बधाई छ!** तपाईंले pandas को आधारभूत कुरा सिक्नुभयो! 🚀

