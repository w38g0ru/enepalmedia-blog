---
layout: post
title: "Python लाईब्रेरी Pandas ट्युटोरियल "
date: 2025-02-13 08:45:12 +0545
---

Pandas भनेको Python मा आधारित एक ओपन सोर्स सफ्टवेयर लाइब्रेरी हो । यसले प्रयोगकर्तालाई spreadsheet मा जस्तै छिटो डेटा लोड गर्न, आवश्यकता अनुसार भिन्न ढाँचामा डेटालाई परिवर्तन गर्न, २ वा २ भन्दा बढी डेटासेटहरुलाई मर्ज गर्ने लगायतका कामहरू गर्नको लागी सहजता प्रदान गर्दछ  । यसले डेटा क्लिनिङ्ग र structured डेटाका ढाँचाहरू जस्तै tables, matrices, र time-series सँग काम गर्न सजिलो बनाउँछ । यो Python का अरु scientific libraries सँग पनि राम्रोसँग काम गर्छ ।

---

## १. pandas इन्स्टल गर्ने र सेटअप गर्ने  
सबैभन्दा पहिले, तपाईंको कम्प्युटरमा pandas लाइब्रेरी **इन्स्टल** गर्नुपर्छ। 

```python
pip install pandas
import pandas as pd
```

`pd` **pandas को संक्षिप्त नाम** हो, जुन प्रायः प्रयोग गरिन्छ।

---

## २. pandas को मुख्य डाटा संरचना (Data Structures)  
प्यान्डासमा Series र DataFrame दुई प्रमुख डेटा स्ट्रक्चरहरु हुन्छन्। वान डाईमेन्सनल डेटा संरचनालाई सिरिज भनिन्छ भने मल्टीडाईमेन्सनल डेटा संरचनालाई डेटाफ्रेम भनिन्छ । वान डाईमेन्सनल डेटा संरचना लिस्ट जस्तो देखिन्छ भने डेटाफ्रेम दुई डाईमेन्सनल संरचना हुन्छ।

```python
import pandas as pd

data = [10, 20, 30, 40]
series = pd.Series(data)
print(series)
```
📌 **आउटपुट:**
```
0    10
1    20
2    30
3    40
dtype: int64
```
🔹 Series मा Index हुन्छ, जुन स्वतः 0,1,2,3... मा सेट हुन्छ।
---

### 🟢 DataFrame बनाउने तरिका  
DataFrame त्यस्तो संरचना खालको संरचना हो जसमा रो (Rows) र कोलम (Columns) हुने गर्दछ । 
```python
data = {
    "नाम": ["राम", "सीता", "गिता", "श्याम"],
    "उमेर": [25, 22, 28, 30],
    "शहर": ["काठमाडौं", "पोखरा", "ललितपुर", "बुटवल"]
}
df = pd.DataFrame(data)
print(df)
```
📌 **आउटपुट:**  
```
    नाम  उमेर     शहर
0   राम    25  काठमाडौं
1  सीता    22   पोखरा
2  गिता    28  ललितपुर
3  श्याम    30   बुटवल
```

---

## ३. DataFrame को बेसिक अपरेशनहरू  

### 🔹 पहिलो पाँच पंक्ति हेर्न (head)
```python
print(df.head())

### 🔹 अन्तिम पाँच row हेर्न (tail)
print(df.tail())

### 🔹 डाटा प्रकार (Data Types) हेर्न
print(df.dtypes)

### 🔹 columns हरूको नाम हेर्न
print(df.columns)

### 🔹 row संख्या र column संख्या हेर्न
print(df.shape)
```

---

## ४. DataFrame बाट डेटा सेलेक्सन (Selection)  

### 🔹 कुनै एक स्तम्भ (Column) चयन गर्ने
```python
print(df["name"])

### 🔹 विशेष पंक्ति (Row) चयन गर्ने
print(df.loc[1])   # दोस्रो Row
print(df.iloc[2])  # तेस्रो Row

### 🔹 विशेष Row र Column सेलेक्ट गर्ने
print(df.loc[0, "city"])  # पहिलो व्यक्तिको शहर
```

१.१. Addition (+)
दुई वा बढी संख्याहरूको जोड़ गर्नको लागि प्रयोग गरिन्छ।
``` python
python
Copy
Edit
a = 10
b = 5
result = a + b
print(result)  # 15
```


१.२. Subtraction (-)
दुई संख्याको घटाउ गर्नको लागि प्रयोग गरिन्छ।

python
Copy
Edit
a = 10
b = 5
result = a - b
print(result)  # 5
१.३. Multiplication (*)
दुई संख्याको गुणा गर्नको लागि प्रयोग गरिन्छ।

python
Copy
Edit
a = 10
b = 5
result = a * b
print(result)  # 50
१.४. Division (/)
दुई संख्याको भाग गर्ने अपरेटर हो, जसले विभाजनको परिणाम फ्लोटिङ पोइन्ट भ्यालु दिन्छ।

python
Copy
Edit
a = 10
b = 5
result = a / b
print(result)  # 2.0
१.५. Floor Division (//)
दुई संख्याको भाग गर्दा केवल पूर्णांक (integer) परिणाम दिने अपरेटर हो।

python
Copy
Edit
a = 10
b = 3
result = a // b
print(result)  # 3
१.६. Modulus (%)
यो अपरेटरले दुई संख्याको भागको बाकी निकाल्छ।

python
Copy
Edit
a = 10
b = 3
result = a % b
print(result)  # 1
१.७. Exponentiation (**)
यो अपरेटरले दुई संख्याको घात निकाल्छ।

python
Copy
Edit
a = 2
b = 3
result = a ** b
print(result)  # 8
२. स्ट्रिङ अपरेसनहरू (String Operations)
Python मा स्ट्रिङ पनि एक प्रमुख डाटा प्रकार हो र यसमा केहि महत्वपूर्ण अपरेसनहरू लागू गर्न सकिन्छ।

२.१. Concatenation (+)
स्ट्रिङहरूलाई जोड्नको लागि + अपरेटर प्रयोग गर्न सकिन्छ।

python
Copy
Edit
str1 = "Hello"
str2 = "World"
result = str1 + " " + str2
print(result)  # Hello World
२.२. Repetition (*)
स्ट्रिङलाई पुनः दोहोर्याउनको लागि * अपरेटर प्रयोग गर्न सकिन्छ।

python
Copy
Edit
str1 = "Hi "
result = str1 * 3
print(result)  # Hi Hi Hi 
२.३. Slicing
स्ट्रिङको कुनै पनि अंशलाई लिनको लागि slicing प्रयोग गर्न सकिन्छ।

python
Copy
Edit
str1 = "Python"
result = str1[1:4]  # Extracts "yth"
print(result)
२.४. Length (len())
स्ट्रिङको लम्बाई (कति अक्षरहरू छन्) पत्ता लगाउन len() फंक्सन प्रयोग गर्न सकिन्छ।

python
Copy
Edit
str1 = "Python"
result = len(str1)
print(result)  # 6
३. लिस्ट अपरेसनहरू (List Operations)
Python मा लिस्टहरू एक महत्वपूर्ण डाटा संरचना हो जसमा विभिन्न प्रकारका डाटा राख्न सकिन्छ। लिस्टमा केही सामान्य अपरेसनहरू निम्नलिखित छन्।

३.१. लिस्टमा आइटम जोड्नु (Appending)
लिस्टमा नयाँ आइटम थप्नको लागि append() मेथड प्रयोग गर्न सकिन्छ।

python
Copy
Edit
my_list = [1, 2, 3]
my_list.append(4)
print(my_list)  # [1, 2, 3, 4]
३.२. लिस्टबाट आइटम हटाउनु (Removing)
लिस्टबाट आइटम हटाउनको लागि remove() मेथड प्रयोग गर्न सकिन्छ।

python
Copy
Edit
my_list = [1, 2, 3, 4]
my_list.remove(3)
print(my_list)  # [1, 2, 4]
३.३. लिस्टको लम्बाई जान्नु (Length of List)
लिस्टको लम्बाई पत्ता लगाउन len() प्रयोग गर्न सकिन्छ।

python
Copy
Edit
my_list = [1, 2, 3]
result = len(my_list)
print(result)  # 3
३.४. लिस्टमा आइटमको स्थान जान्नु (Indexing)
लिस्टमा कुनै आइटमको स्थान जान्नको लागि index() मेथड प्रयोग गर्न सकिन्छ।

python
Copy
Edit
my_list = [1, 2, 3]
result = my_list.index(2)
print(result)  # 1
४. तुलना अपरेसनहरू (Comparison Operations)
Python मा विभिन्न प्रकारका तुलना अपरेसनहरू छन् जसले दुई भेरिएबलहरूको तुलनासम्बन्धी परिणाम दिन्छ। यी अपरेसनहरू Boolean मानहरू (True या False) दिन्छ।

४.१. समानता (==)
दुई मान समान छन् कि छैन भनेर परीक्षण गर्नको लागि == प्रयोग गर्न सकिन्छ।

python
Copy
Edit
a = 5
b = 5
result = a == b
print(result)  # True
४.२. असमानता (!=)
दुई मान असमान छन् कि छैन भनेर परीक्षण गर्नको लागि != प्रयोग गर्न सकिन्छ।

python
Copy
Edit
a = 5
b = 3
result = a != b
print(result)  # True
४.३. ठूलो, सानो, र समकक्ष (> , < , >= , <=)
दुई मानको तुलनात्मक जाँच गर्नको लागि यी अपरेसनहरू प्रयोग गर्न सकिन्छ।

python
Copy
Edit
a = 5
b = 3
result = a > b
print(result)  # True
५. Logical अपरेसनहरू (Logical Operations)
Logical operations को मद्दतले हामी दुई वा बढी सर्तहरूको बिचमा सम्बन्ध जाँच गर्न सक्छौं।

५.१. AND (and)
यसले दुई सर्त साँचो भए मात्र साँचो परिणाम दिन्छ।

python
Copy
Edit
a = True
b = False
result = a and b
print(result)  # False
५.२. OR (or)
यसले कुनै एक सर्त साँचो भए मात्र साँचो परिणाम दिन्छ।

python
Copy
Edit
a = True
b = False
result = a or b
print(result)  # True
५.३. NOT (not)
यसले सर्तको उल्टो परिणाम दिन्छ।

python
Copy
Edit
a = True
result = not a
print(result)  # False

---

## ५. फिल्टरिंग (Filtering) – कन्डिसनल सिलेक्शन  
### 🔹 २५ वर्षभन्दा बढी उमेर भएका व्यक्तिहरू छनोट गर्ने  
```python
print(df[df["उमेर"] > 25])
```
