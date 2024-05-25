---
layout: post
title:  "पाइथन (pandas लाईब्रेरी) को प्रयोग गरेर डेटा क्लिन गर्ने तरिका"
date:   2024-05-24 15:38:12 +0545
---
### Pandas डाटा सफाई र अन्वेषण ट्युटोरियल

यो ट्युटोरियलले Pandas लाई प्रयोग गरेर Python मा डाटा कसरी सफा गर्ने र अन्वेषण गर्ने भन्ने बारे बताउँछ। हामीले आधारभूत आयात, डाटा सफा गर्ने तरिकाहरू, र डाटाको बारेमा बुझ्नको लागि केही विधिहरू समेटेका छौं।

#### आधारभूत आयात र उपनामकरण
सुरुमा, आवश्यक पुस्तकालयहरू आयात गरौं र Pandas लाई DataFrame मा सबै स्तम्भहरू र पंक्तिहरू देखाउन कन्फिगर गरौं।

<pre>
import numpy as np
import pandas as pd
</pre>


# DataFrame ट्रन्केशनलाई रोक्न Pandas प्रदर्शन विकल्पहरू समायोजन गरौं
<pre>
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
</pre>

#### डाटा रिड (read) गर्ने तरिका
Pandas ले तपाइँलाई विभिन्न ढाँचाहरूबाट डाटा पढ्न अनुमति दिन्छ, जस्तै CSV, JSON, र TSV। तल यी ढाँचाहरूबाट डाटा कसरी पढ्ने भन्ने उदाहरणहरू छन्:

# CSV मा पढ्ने
<pre>
df = pd.read_csv('some_url_or_filepath.csv')
print(df.head())
</pre>

# JSON मा पढ्ने
df = pd.read_json('some_url_or_filepath.json')
print(df.head())

# TSV मा पढ्ने
df = pd.read_csv('some_url_or_filepath.tsv', delimiter='\t', encoding='utf-8')
print(df.head())

# फाइल अपलोड गर्दै (Google Colab को लागि)
from google.colab import files
upload = files.upload()

# अपलोड गर्दा हेडरहरूको नाम परिवर्तन गर्नुहोस्
url = 'some_url_or_filepath.csv'
df = pd.read_csv(url, names=['column1', 'column2', 'column3'])
```

#### डाटा सफा गर्ने तरिका
डाटा सफा गर्नका लागि धेरै चरणहरू समावेश छन्, जस्तै स्तम्भहरूको नाम परिवर्तन गर्ने, मानहरू प्रतिस्थापन गर्ने, र हराइरहेको डाटालाई ह्यान्डल गर्ने।

```python
# पढ्ने बेला स्तम्भहरूको नाम परिवर्तन गर्नुहोस्
df = pd.read_csv(df, header=None)
feature_map = {0: 'column1', 1: 'column2', 2: 'column3'}
df.rename(columns=feature_map, inplace=True)

# नयाँ मानको साथ डाटासेटमा मानहरू प्रतिस्थापन गर्नुहोस्
df = df.replace('?', np.NaN)

# द्रुत अपरेशनको लागि 'category' प्रकारमा सेट गर्नुहोस्
df['column1'] = df['column1'].astype('category')

# लेबल इन्कोडिङ
df['column1'] = df['column1'].cat.codes

# वन हॉट इन्कोडिङ
df = pd.get_dummies(df, columns=['column1'], prefix=['column1'])
df.head()

# बाइनरी इन्कोडिङ (category_encoders आवश्यक छ)
!pip install category_encoders
import category_encoders as ce
encoder = ce.BinaryEncoder(cols=['column1'])
df = encoder.fit_transform(df)

# हराइरहेको मानहरू भर्नुहोस्
df.fillna(0)  # मानहरूसँग खालीहरू भर्नुहोस्
df.fillna(method='ffill')  # विधिको आधारमा भर्नुहोस्
df.fillna(value={'A': 0, 'B': 1, 'C': 2, 'D': 3})  # प्रत्येक सुविधा फरक मानले भर्नुहोस्

# खाली मानहरू हटाउनुहोस्
df.dropna()  # पंक्तिहरू हटाउनुहोस्
df.dropna(axis='columns')  # स्तम्भहरू हटाउनुहोस्
df.dropna(axis='rows', thresh=3)  # थ्रेसहोल्ड भन्दा कम नन्-नल्स भएका पंक्तिहरू हटाउनुहोस्

# नयाँ स्तम्भ थप्नुहोस्
df['new_feature'] = 'Value'  # सबै पंक्तिहरूको लागि एउटै मानको साथ नयाँ स्तम्भ
df['new_feature'] = df2['df2_feature']  # अर्को DataFrame स्तम्भबाट नयाँ स्तम्भ

# स्तम्भ वा पंक्ति हटाउनुहोस्
df.drop('column1', axis='columns')

# दुई DataFrame हरूलाई संयोजन गर्नुहोस्
df3 = df1.append(df2)

# np.where प्रयोग गरेर अर्को कोटिगरीको मानहरूमा आधारित कोटिगरी इन्कोड गर्नुहोस्
df['column1'] = np.where(df['column2'].str.contains('value'), 1, 0)

# संख्या वा श्रेणीगत आधारित मानहरू अनुमान गर्न लूप प्रयोग गर्नुहोस्
from pandas.api.types import is_numeric_dtype

for column in df:
    if is_numeric_dtype(df[column]):
        # यहाँ संख्यात्मक सुविधाहरूको साथ केहि गर्नुहोस्
    else:
        # यहाँ श्रेणीगत सुविधाहरूको साथ केहि गर्नुहोस्

# स्तम्भलाई datetime मा कास्ट गर्नुहोस्
df['column1'] = pd.to_datetime(df['column1'])

# स्तम्भको प्रकार परिवर्तन गर्नुहोस्
df['column1'] = df['column1'].astype(int)

# धेरै स्तम्भहरू हटाउनुहोस्
df = df.drop(['column1', 'column2'], axis='columns')

# स्तम्भलाई सूचकांकको रूपमा सेट गर्नुहोस्
df = df.set_index('column1')
```

#### डाटा अन्वेषण गर्ने तरिका
डाटा सफा गरेपछि, तपाइँ विभिन्न pandas विधिहरू प्रयोग गरेर डाटाको संरचना र सामग्रीहरू बुझ्न यसको अन्वेषण गर्न सक्नुहुन्छ।

```python
# DataFrame मा पहिलो X पंक्तिहरू देखाउनुहोस्, कुनै मूल्य डिफल्ट 5 हुन्छ
df.head(1)

# DataFrame मा अन्तिम X पंक्तिहरू देखाउनुहोस्, कुनै मूल्य डिफल्ट 5 हुन्छ
df.tail(1)

# DataFrame को सारांश
df.info()

# कुनै पनि संख्यात्मक सुविधाहरूमा आधारभूत तथ्यांकहरू प्राप्त गर्नुहोस्
df.describe()

# DataFrame को आयामहरू
df.shape

# विभिन्न सुविधाहरूको डाटा प्रकारहरू
df.dtypes

# सूचकांक मानहरूको सूची फिर्ता गर्नुहोस्
df.index

# DataFrame को प्रत्येक सुविधामा कति वस्तुहरू छन् गन्नुहोस्
df.count()

# सुविधामा प्रत्येक वस्तु कति छ गन्नुहोस्
df['column1'].value_counts()

# श्रेणीमा कति अद्वितीय मानहरू छन् गन्नुहोस्
df['column1'].value_counts().count()
df['column1'].nunique()

# श्रेणीमा सबै अद्वितीय मानहरूको सूची फिर्ता गर्नुहोस्
df['column1'].unique()

# कति खाली वा नन-खाली मानहरू छन् र कुन सुविधाहरूमा छन्
df.isnull().sum()
df.notnull().sum()

# लेबल द्वारा स्तम्भहरू वा पंक्तिहरू पहुँच गर्नुहोस्
df.loc['column_or_index_name']

# पूर्णांक स्थिति द्वारा स्तम्भहरू वा पंक्तिहरू पहुँच गर्नुहोस्
df.iloc[5]

# पंक्ति/स्तम्भ जोडीबाट एकल मान पहुँच गर्नुहोस्
df.at[2, 'column3']

# शब्दकोश अनुसार श्रेणीमा मानहरू म्याप गर्नुहोस्
df['column1'].map({'value1': 'value11', 'value2': 'value22'})

# दुई मानहरूको बीचमा भएका पंक्तिहरूको boolean भेक्टर फिर्ता गर्नुहोस्
df['column1'].between(1, 5, inclusive=True)

# श्रेणी वा स्केलर भन्दा बढी भएका पंक्तिहरूको boolean भेक्टर फिर्ता गर्नुहोस्
df['column1'].gt(5)
df['column1'].gt(df['column2'])

# श्रेणी वा स्केलर भन्दा कम भएका पंक्तिहरूको boolean भेक्टर फिर्ता गर्नुहोस्
df['column1'].lt(5)
df['column1'].lt(df['column2'])

# केवल मानहरू फिर्ता गर्नुहोस्, सूचकांक र स्तम्भ लेबलहरू ड्रप हुन्छ
df.to_numpy()

# DataFrame को अक्षमा कार्य लागू गर्नुहोस्
df.apply(np.sum, axis='index')

# DataFrame लाई ट्रान्सपोज गर्नुहोस् (स्तम्भहरू सूचकांक बन्ने, सूचकांक स्तम्भ बन्ने)
df.T

# थप उपयोगी pandas कलहरू
df.groupby()  # स्तम्भ द्वारा डाटा समूह गर्नुहोस्
df.interpolate()  # हराइरहेको डाटा इन्टरपोल गर्नुहोस्

# pd.cut को साथ बिनिङ
bins = pd.cut(df['column1'], 5)  # 5 बिनहरू बनाउनुहोस्

# छिटो साना तालिकाहरूको लागि क्रसट्याब
pd.crosstab(bin_or_feature, bin_or_feature, normalize='columns')

# पिभट तालिका
table = pd.pivot_table(df, values=['column1'], index=['column2'], columns=['column3'])
table = pd.pivot_table(df, values=['column1'], index=['column2'], columns=['column3'], aggfunc=np.sum)
```

यस ट्युटोरियलले Pandas प्रयोग गरेर डाटा सफा गर्ने र अन्वेषण गर्ने महत्वपूर्ण तरिकाहरू समेट्छ, जसले तपाइँलाई उन्नत डाटा विश्लेषण कार्यहरू गर्नको लागि राम्रो आधार प्रदान गर्दछ।
