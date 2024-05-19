---
layout: post
title:  "प्रेस काउन्सिलले सुचीकृत गरेका अनलाईनहरुको बिबररण - .py series-1"
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

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/Enlisted-Online-Media-List-Excel.xlsx)  यसले पिडिएफ फाइललाई एक्सलमा कन्भर्ट गर्दछ । यद्यपि एक्सल फाइलको डाटाहरू भद्रगोल छन् । कतै पहिलो दुई वटा कोलम खाली छन् कुनै कुनैमा पहिलो कोलम बाट डेटा सुरु हुन्छ कुनैमा दोस्रो कोलम बाट । अब हाम्रो काम भनेको डाटालाई ठ्याक्क मिलाएर राख्नु पनि हो । डाटा एक्सलमा भएको हुनाले तपाई आफ्नो इच्छा अनुसार यसलाई म्यान वली पनि गर्न सक्नु हुन्छ । तर हामी पाईथन सिक्दै गरेको हुनाले यो काम पाईथन कोड लेखेर गर्छौ ।

<pre>
import pandas as pd

# Read the Excel file
df = pd.read_excel("Enlisted-Online-Media-List-Excel.xlsx")

# Function to shift non-empty cells to the left in each row
def shift_cells(row):
    shifted_row = row[row.notnull()].tolist()
    shifted_row.extend([None] * (len(row) - len(shifted_row)))
    return pd.Series(shifted_row, index=row.index)

# Shift cells in each row
df = df.apply(shift_cells, axis=1)

# Write the modified DataFrame to a new Excel file
df.to_excel("shift-non-empty-cells-to-the-left.xlsx", index=False)
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/shift-non-empty-cells-to-the-left.xlsx) यसल प्रत्येक row भएका non-empty cells लाई बायाँतिर सर्छ र empty cells लाई दायाँतिर पठाउँछ।

<pre>
import pandas as pd

# Read the Excel file
df = pd.read_excel("shift-non-empty-cells-to-the-left.xlsx")

# Drop rows where the third column (index 2 in zero-based indexing) is empty
df = df.dropna(subset=[df.columns[4]])

# Write the modified DataFrame to a new Excel file
df.to_excel("drop-rows-where-the-third-column(zero-based indexing)-is-empty.xlsx", index=False)
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/drop-rows-where-the-third-column(zero-based indexing)-is-empty.xlsx)  माथिको कोडले यदि कुनै रो (row) मा वेब ठेगाना छैन भने त्यो रो (row) पुरै डिलिट गर्दिन्छ । पिडिएफ बाट एक्सलमा कन्भर्ट गर्ने क्रममा खाली रो हरू आएका पनि हुन सक्छन । हामीले माथी जेनेरेट गरेको फाईलमा चौथो कोलममा युआरएल छन । 

<pre>
import pandas as pd

file_path = 'drop-rows-where-the-third-column(zero-based indexing)-is-empty.xlsx'

# Load the Excel file into a DataFrame
df = pd.read_excel(file_path)

# Define a list of shifts with row range and direction (left or right)
shifts = [
    (range(1986, 1992), 'right'),  # Range of rows
    (range(1993, 1996), 'right'),  # Range of rows
    (range(1998, 2010), 'right'),  # Range of rows
    (range(2011, 2014), 'right'),  # Range of rows
    (range(2015, 2019), 'right'),  # Range of rows
    (37, 'right')  # Individual row
]

for shift in shifts:
    rows, direction = shift
    if isinstance(rows, range):
        for row in rows:
            if direction == 'left':
                df.iloc[row, :-1] = df.iloc[row, 1:].values
                df.iloc[row, -1] = None  # Optional: clear the last cell
            elif direction == 'right':
                df.iloc[row, 1:] = df.iloc[row, :-1].values
                df.iloc[row, 0] = None  # Optional: clear the first cell
    else:
        row = rows
        if direction == 'left':
            df.iloc[row, :-1] = df.iloc[row, 1:].values
            df.iloc[row, -1] = None  # Optional: clear the last cell
        elif direction == 'right':
            df.iloc[row, 1:] = df.iloc[row, :-1].values
            df.iloc[row, 0] = None  # Optional: clear the first cell

# Save the modified DataFrame to a new Excel file
df.to_excel('shift-the-entire-row-left-or-right.xlsx', index=False)
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/shift-the-entire-row-left-or-right.xlsx) माथीको कोडले एउटै कोलममा नपरेका डाटाहरुलाई एउटै कोलममा सार्ने काम गर्दछ । 

<pre>
from openpyxl import load_workbook

# Load the Excel file
wb = load_workbook('shift-the-entire-row-left-or-right.xlsx')
ws = wb.active

# Define a mapping for Kantipur numbers to English numbers
kantipur_to_english = {
    ')': '0', '!': '1', '@': '2', '#': '3', '$': '4',
    '%': '5', '^': '6', '&': '7', '*': '8', '(': '9',
}

# Iterate over all cells in the 'MOBILE' column and convert Kantipur numbers to English numbers
for row in ws.iter_rows(min_row=2, max_row=ws.max_row, min_col=8, max_col=8):  # Assuming 'MOBILE' is the 9th column
    for cell in row:
        if isinstance(cell.value, str):
            converted_chars = []
            for char in cell.value:
                if char in kantipur_to_english:
                    converted_chars.append(kantipur_to_english[char])
                else:
                    converted_chars.append(char)
            cell.value = ''.join(converted_chars)

# Save the modified Excel file
wb.save('List-with-Kantipur-numbers-to-English-numbers.xlsx')

</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/List-with-Kantipur-numbers-to-English-numbers.xlsx)  यो कोडले हामीले काम गर्दै गरेको एक्सल फाईलको आठौ रो मा भएको मोबाईल नम्बरलाई अंग्रेजीमा रुपान्तरण गर्ने काम गर्दछ । 

<pre>
import pandas as pd

# Read the Excel file
df = pd.read_excel("List-with-Kantipur-numbers-to-English-numbers.xlsx")

# Keep columns up to 'I' and drop all columns after 'I'
columns_to_keep = df.columns[:df.columns.get_loc('Unnamed: 4') + 1]
df = df[columns_to_keep]

# Save the updated DataFrame to a new Excel file
df.to_excel("drop-all-columns-after-I.xlsx", index=False)
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/drop-all-columns-after-I.xlsx)  माथीको कोडले डाटा भएको अन्तिम कोलम (I) पछीका सबै कोलमहरु डिलिट गर्ने काम गर्दछ । 

<pre>
import pandas as pd

# Read the Excel file
df = pd.read_excel("drop-all-columns-after-I.xlsx")

# Split the values in column H (phone numbers) into separate columns
phone_numbers_split = df['cgnfOgsf gfd'].str.split(',', expand=True)
phone_columns = [f'Phone_{i+1}' for i in range(phone_numbers_split.shape[1])]
df[phone_columns] = phone_numbers_split

# Split the values in column I (email addresses) into separate columns
email_addresses_split = df['Unnamed: 4'].str.split(',', expand=True)
email_columns = [f'Email_{i+1}' for i in range(email_addresses_split.shape[1])]
df[email_columns] = email_addresses_split

# Optional: Drop the original H and I columns if no longer needed
# df.drop(columns=['H', 'I'], inplace=True)


# Save the updated DataFrame to a new Excel file
df.to_excel("split-the-values-in-column-H-and-I-into-separate-columns.xlsx", index=False)
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/split-the-values-in-column-H-and-I-into-separate-columns.xlsx)  यो कोडले ईमेल र मोबाईल कोलमममा भएका टेक्स्टहरुलाई त्यसको भएको कमा को आधारमा छुट्टयार अन्तिमको कोलममा राख्ने काम गर्दछ । 

<pre>
import pandas as pd

# Read the Excel file
df = pd.read_excel("split-the-values-in-column-H-and-I-into-separate-columns.xlsx")

# Print original headers
print("Original Headers:", df.columns.tolist())

# Rename the headers
df.rename(columns={"Unnamed: 0": "SN", "kmfOn g=": "REG_NO","Unnamed: 1":"RED_DATE_NP","btf g=":"URL","Unnamed: 2":"PUBLICATION","btf ldlt":"ADDRESS","Unnamed: 3":"PUBLISHER","cgnfOgsf gfd":"CONTACT","Unnamed: 4":"EMAIL"}, inplace=True)

# Print new headers
# print("New Headers:", df.columns.tolist())
# Save the updated DataFrame to a new Excel file
df.to_excel("rename-the-headers-all-data.xlsx", index=False)

</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/rename-the-headers-all-data.xlsx) माथीको कोडले अहिले सम्म हामीले काम गर्दै गरेको एक्सल फाईलको हेडीङ्ग परिवर्तन गर्दछ । 

<pre>
import pandas as pd

# Read the Excel file
df = pd.read_excel('rename-the-headers-all-data.xlsx')

# Convert the DataFrame to JSON
json_data = df.to_json(orient='records', lines=True)

# Write the JSON data to a file
with open('rename-the-headers-all-data.json', 'w') as f:
    f.write(json_data)
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस](https://districts.enepal.net.np/rename-the-headers-all-data.json)  एक्सल फाईल फाईललाई जेसनमा परिवर्तन गर्दछ । 

<pre>
import pandas as pd

# Load the Excel file
file_path = 'rename-the-headers-all-data.xlsx'
df = pd.read_excel(file_path, sheet_name='Sheet1')

# Group the data by the first 4 digits of REG_DATE
grouped = df.groupby(df['RED_DATE_NP'].astype(str).str[:4])

# Create a new Excel file for each group
with pd.ExcelWriter('group-the-data-by-the-reg-year.xlsx') as writer:
    for name, group in grouped:
        # Write each group to a separate sheet
        group.to_excel(writer, sheet_name=f'BS_{name}', index=False)

print("Data divided into separate sheets based on the 4-digit numbers in column D.")
</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/group-the-data-by-the-reg-year.xlsx)  माथी कोडले एउटै सिटमा भएका सबै डाटाहरुलाई रजिष्ट्रेशन डेट (नेपाली) को आधारमा छुट्टा छुट्टै सिटमा डाटाहरु राख्ने काम गर्दछ । 

<pre>
import pandas as pd
import whois
from datetime import datetime

# Read the Excel file and the specific sheet
df = pd.read_excel('group-the-data-by-the-reg-year.xlsx', sheet_name='BS_2070')

# Initialize lists to store WHOIS information
whois_data = {
    'Registrar': [],
    'Whois_Server': [],
    'Referral_URL': [],
    'Updated_Date': [],
    'Creation_Date': [],
    'Expiration_Date': [],
    'Name_Servers': [],
    'Status': [],
    'Emails': [],
    'Dnssec': [],
    'Name': [],
    'Org': [],
    'Address': [],
    'City': [],
    'State': [],
    'Registrant_Postal_Code': [],
    'Country': []
}

# Helper function to format dates
def format_date(date):
    if isinstance(date, list):
        return [d.strftime('%d-%m-%Y') if isinstance(d, datetime) else None for d in date]
    return date.strftime('%d-%m-%Y') if isinstance(date, datetime) else None

# Fetch WHOIS information for each domain
for domain in df['URL']:
    try:
        domain_info = whois.whois(domain)
        whois_data['Registrar'].append(domain_info.registrar)
        whois_data['Whois_Server'].append(domain_info.whois_server)
        whois_data['Referral_URL'].append(domain_info.referral_url)
        whois_data['Updated_Date'].append(format_date(domain_info.updated_date))
        whois_data['Creation_Date'].append(format_date(domain_info.creation_date))
        whois_data['Expiration_Date'].append(format_date(domain_info.expiration_date))
        whois_data['Name_Servers'].append(domain_info.name_servers)
        whois_data['Status'].append(domain_info.status)
        whois_data['Emails'].append(domain_info.emails)
        whois_data['Dnssec'].append(domain_info.dnssec)
        whois_data['Name'].append(domain_info.name)
        whois_data['Org'].append(domain_info.org)
        whois_data['Address'].append(domain_info.address)
        whois_data['City'].append(domain_info.city)
        whois_data['State'].append(domain_info.state)
        whois_data['Registrant_Postal_Code'].append(domain_info.registrant_postal_code)
        whois_data['Country'].append(domain_info.country)
    except whois.parser.PywhoisError as e:
        print(f"Error fetching WHOIS info for {domain}: {e}")
        # Append None for all columns if there is an error
        for key in whois_data.keys():
            whois_data[key].append(None)

# Create a new DataFrame for WHOIS data
whois_df = pd.DataFrame(whois_data)

# Find the index of the Email_3 column to place the WHOIS data next to it
email_3_index = df.columns.get_loc('Email_3') + 1

# Insert the WHOIS data into the original DataFrame at the specified location
df_updated = pd.concat([df.iloc[:, :email_3_index], whois_df, df.iloc[:, email_3_index:]], axis=1)

# Write the updated DataFrame back to the same Excel file and sheet
with pd.ExcelWriter('group-the-data-by-the-reg-year.xlsx', mode='a', if_sheet_exists='replace') as writer:
    df_updated.to_excel(writer, sheet_name='BS_2070', index=False)

</pre>

[माथीको कोडले तयार गरेेको फाईल हेर्न यहाँ क्लिक गर्नुहोस ।](https://districts.enepal.net.np/group-the-data-by-the-reg-year.xlsx) माथीको कोडले छुट्टा छु्ट्टै सिटमा भएको वेबसाईट ठेगाना () को आधारमा त्यसको डेटा तान्ने काम गर्दछ । यसको लागि पाईथन मोड्युलको प्रयोग गरीएको छ । यसो गर्दा सबै भन्दा माथीको सिटको नाम र तलको सिटको नाम एकै पटक परिवर्तन गर्नु पर्दछ । यसरि छुट्टा छुट्टै सिटमा राख्नुको कारण पनि हुई डाटा तान्ने काम क्रमश होस । एकै पटक सर्भरलाई लोड नपरोस भन्नाले हो । 

<pre>
import pandas as pd

# Load all sheets into a dictionary of DataFrames
xls = pd.ExcelFile('group-the-data-by-the-reg-year.xlsx')
dfs = {sheet_name: xls.parse(sheet_name) for sheet_name in xls.sheet_names}

# Concatenate all DataFrames into one
df_all = pd.concat(dfs.values(), ignore_index=True)

# Write the concatenated DataFrame to a new sheet in the same Excel file
with pd.ExcelWriter('group-the-data-by-the-reg-year.xlsx', mode='a', if_sheet_exists='replace') as writer:
    df_all.to_excel(writer, sheet_name='ALL', index=False)
</pre>

