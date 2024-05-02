---
layout: post
title:  "डाउनलोड फोल्डरमा भएका फाइलहरू व्यवस्थापन गर्ने पाइथन स्क्रिप्ट"
date:   2024-03-08 10:10:10 +0545
---
<p>
यो Python स्क्रिप्टले फाइलहरूलाई त्यसको फाइल एक्सटेन्सनमा आधारमा डोकुमेन्ट्स फोल्डरको विशेष फोल्डरहरूमा सञ्चालित गर्दछ, आवश्यक छ भने गन फोल्डरहरू सिर्जना गर्दछ, र यदि डुप्लिकेटहरू पाइन्छन् भने फाइल नामहरूमा एक समय मिलाउँदछ। अन्तिम रुपमा, यो डाउनलोड्स फोल्डरबाट मूल फाइलहरूलाई हटाउँदछ।</p>
<pre>
import os
import shutil
import time

# Path to the Downloads folder
downloads_folder = os.path.expanduser("~/Downloads/Documents")

# Path to the Documents folder
documents_folder = os.path.expanduser("~/Documents")

# Dictionary mapping file extensions to folder names
extension_folders = {
    "doc": "Docs",
    "docx": "Docs",
    "xls": "Sheets",
    "xlsx": "Sheets",
    "pdf": "PDF",
    "zip": "Zip",
    "jpg": "Images",
    "jpeg": "Images",
    "png": "Images",
    "gif": "Images"
}

# Create the destination folders if they don't exist
for folder_name in set(extension_folders.values()):
    folder_path = os.path.join(documents_folder, folder_name)
    os.makedirs(folder_path, exist_ok=True)

# Create the 'Other' folder if it doesn't exist
other_path = os.path.join(documents_folder, "Other")
os.makedirs(other_path, exist_ok=True)

# Move files from the Downloads folder to the Documents folder
for file_name in os.listdir(downloads_folder):
    file_path = os.path.join(downloads_folder, file_name)
    if os.path.isfile(file_path):
        extension = file_name.split(".")[-1]
        destination_folder = extension_folders.get(extension, "Other")
        destination_path = os.path.join(documents_folder, destination_folder, file_name)
        while os.path.exists(destination_path):
            timestamp = int(time.time())
            new_name = f"{os.path.splitext(file_name)[0]}_{timestamp}{os.path.splitext(file_name)[1]}"
            destination_path = os.path.join(documents_folder, destination_folder, new_name)
        shutil.move(file_path, destination_path)
        print(f"Moved {file_name} to {destination_path}")

# Print message after moving files
print("All files moved successfully.")

# Delete files from the Downloads folder
for file_name in os.listdir(downloads_folder):
    file_path = os.path.join(downloads_folder, file_name)
    if os.path.isfile(file_path):
        os.remove(file_path)
        print(f"Deleted {file_name}")

# Print message after deleting files
print("All files deleted from Downloads folder.")
</pre>
