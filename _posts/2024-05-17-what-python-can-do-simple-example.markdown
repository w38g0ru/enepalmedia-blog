---
layout: post
title:  "पाइथन बाट सजिलै गर्न सकिने एउटा काम"
date:   2024-05-17 20:38:12 +0545
---
युजकेस सिनारियो : नेपाल प्रेस काउन्सिलले नियमित रूपमा प्रक्रिया पुरा गरी सञ्चालनमा रहेका अनलाइन वेबसाईटहरुको नामावली प्रकाशन गर्दछ । नामावली पिडिएफ फाईलमा प्रकाशन भएको हुन्छ । जसमा वेबसाइटको ठेगाना http प्रोटोकल बिना ठ्याक्क डोमेन नेम र एक्सटेन्सन मात्र लेखिएको हुन्छ भने वेबसाइट सञ्चालकको नाम , प्रकाशन गृह (कम्पनी), मोबाइल नम्बर र इमेल ठेगाना राखिएको हुन्छ । मोबाइल नम्बर पनि कसैको २ वटा , कसैको १ वटा , कसैको मोबाइल नम्बरको सट्टामा ल्यान्ड लाइन मोबाइल नम्बर र इमेल ठेगाना कसैको २ वटा कसैको १ वटा त्यो पनि एउटा सेलमा रहेको हुन्छ । पाईथनको साहायताले हामी यो डाटा क्लिन गर्नुका साथै यसको हुईज रेकर्ड पनि तान्छौ । अनि आगामी महिना एक्सपायर हुने डोमेनहरूको विवरण निकाल्छौ । मलाई लाग्छ - यती गरी सक्दा पाईथनबाट गर्न सकिने धेरै कामको आइडिया हुन्छ - त्यसपछी हामी जसो भन्यो त्यसै गर्न सक्छौ । 

यसको लागि सबैभन्दा पहिले हामीले प्रेसकाउन्सिल ले उपलब्ध गराएको डाटा (जुन पिडिएफ फाईल) मा हुन्छ त्यसलाई माईक्रोसफ्ट एक्सल फर्माट (xlsx) मा एक्सपोर्ट गर्दछौ । यो ट्युटोरियल तयार गर्दा सम्मको [बिबरण](https://www.presscouncilnepal.gov.np/np/wp-content/uploads/2024/04/Enlisted-Online-Media-till-2081-01-04.pdf) मा भेट्न सकिन्छ तर यो लिङ्क ब्रेक हुन सक्ने सम्भावना पनि उत्तिकै रहेकोले यसलाई हामी [क्लाउड फ्लेयरमा अपलोड गरेर राखेका छौ](https://districts.enepal.net.np/Enlisted-Online-Media-till-2081-01-04.pdf) । 

<pre>
# Install necessary libraries
# !pip install tabula-py pandas

import requests
import tabula
import pandas as pd

# Download the PDF file
pdf_url = "https://districts.enepal.net.np/Enlisted-Online-Media-till-2081-01-04.pdf"
response = requests.get(pdf_url, headers={'User-Agent': 'Mozilla/5.0'})
local_pdf_path = "Enlisted-Online-Media.pdf"

with open(local_pdf_path, 'wb') as file:
    file.write(response.content)

# Read and combine tables from the downloaded PDF
tables = tabula.read_pdf(local_pdf_path, pages='all', multiple_tables=True)
combined_df = pd.concat(tables, ignore_index=True)

# Write the combined DataFrame to a single sheet in the Excel file
combined_df.to_excel("Enlisted-Online-Media-List-Excel.xlsx", index=False)
</pre>

माथीको कोडले पिडिएफ फाईललाई एक्सलमा कन्भर्ट गर्दछ । यद्दपी एक्सल फाईलको डाटाहरु भद्रगोल हुन्छ । पहिलो दुईवटा कोलम खाली हुन्छन कुनै क्रस कुनैमा पहिलो कोलम बाट शुरु हुन्छ कुनैमा दोस्रो रो बाट । अब हाम्रो काम भनेको डाटालाई ठ्याक्क एक खालको डाटा एउटै कोलममा रहने गरी मिलाएर राख्नु हो । डाटा एक्सलमा भए हुनाले तपाई आफ्नो ईच्छा अनुसार यसलाई म्यानुवली पनि गर्न सक्नु हुन्छ । तर हामी पाईथन सिक्दै गरेको हुनाले यो काम पाईथन कोड लेखेर नै गरौ । 
