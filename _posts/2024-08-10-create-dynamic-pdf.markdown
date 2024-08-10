---
layout: post
title:  "JSON डाटा बाट PDF फाईल बनाउने तरिका"
date:   2024-08-10 00:38:12 +0545
---
तपाईंले दिएको कोडले एउटा इन्टरएक्टिव PDF फर्म क्रियट गर्ने गर्न गर्दछ । यसमा विभिन्न प्रश्नहरू छन त्यस प्रश्नको ठ्याक्क मुनी २ वटा टेक्स्ट बक्सहरू छन । यसले ReportLab लाईब्रेरीको प्रयोग गरी PDF फाइल बनाउँछ, जसमा शीर्षक, अप्सन, र उत्तरका लागि टेक्स्ट बक्सहरू समावेश गरीएको छ ।

यहाँ मुख्य काम भनेको create_pdf_form भन्ने फङ्गसन हो, जसले JSON डेटा लोड गर्छ र त्यसलाई PDF मा रूपान्तरण गर्छ । यसमा विभिन्न प्रश्नहरूको लागि क्रमबद्ध शीर्षक र अप्सनहरुहरू राखिएको छ, र प्रत्येक प्रश्नको लागि दुई वटा टेक्स्ट बक्सहरू बनाईएको छ । एउटा टेक्स्ट बक्समा प्रश्नको अर्थ लेख्न सोधेको छ भने अर्कोमा उत्तर।

``` python
!pip install reportlab
from reportlab.pdfgen import canvas
from reportlab.lib.pagesizes import A4
from reportlab.pdfbase import pdfform
from reportlab.lib.colors import black, lightgrey
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.platypus import Paragraph
from reportlab.lib.units import mm
import json

def create_pdf_form(json_data, output_filename):
    c = canvas.Canvas(output_filename, pagesize=A4)
    width, height = A4

    # Define styles
    styles = getSampleStyleSheet()
    normal_style = ParagraphStyle('Normal', fontName='Helvetica', fontSize=10, leading=14)
    title_style = ParagraphStyle('Title', fontName='Helvetica-Bold', fontSize=14, leading=18, spaceAfter=6)

    # Define margins
    left_margin = 20*mm
    right_margin = width - 20*mm
    top_margin = height - 30*mm
    bottom_margin = 20*mm
    y = top_margin

    field_counter = 0

    # Add a header to each page
    def header(canvas, doc):
        canvas.saveState()
        canvas.setFont('Helvetica-Bold', 16)
        canvas.drawString(left_margin, top_margin + 10*mm, "Patient Data Form")
        canvas.setStrokeColor(lightgrey)
        canvas.setLineWidth(0.5)
        canvas.line(left_margin, top_margin + 7*mm, right_margin, top_margin + 7*mm)
        canvas.restoreState()

    header(c, None)

    def draw_text_with_options(index, title, options):
        nonlocal y
        # Check if we need to start a new page
        if y < bottom_margin + 80*mm:
            c.showPage()
            y = top_margin
            header(c, None)

        # Draw serial number and title
        title_text = f"{index}. {title}"
        title_paragraph = Paragraph(title_text, title_style)
        title_paragraph.wrap(right_margin - left_margin, 20*mm)
        title_paragraph.drawOn(c, left_margin, y - 6*mm)
        y -= title_paragraph.height + 4*mm

        # Draw options
        if options:
            for option in options:
                option_paragraph = Paragraph(f"• {option}", normal_style)
                option_paragraph.wrap(right_margin - left_margin - 10*mm, 20*mm)
                option_paragraph.drawOn(c, left_margin + 5*mm, y - 5*mm)
                y -= option_paragraph.height + 1*mm
            y -= 5*mm

        # Add "What do you understand by this question?" text box
        c.setFont("Helvetica", 10)
        c.drawString(left_margin, y, "What do you understand by this question?")
        y -= 7*mm
        field_name = f"understand_{field_counter}"
        pdfform.textFieldRelative(c, field_name, left_margin, y - 20*mm, right_margin - left_margin, 20*mm)
        y -= 25*mm

        # Add "Source of the Information (Answer)" text box
        c.drawString(left_margin, y, "Source of the Information (Answer)")
        y -= 7*mm
        field_name = f"source_{field_counter}"
        pdfform.textFieldRelative(c, field_name, left_margin, y - 20*mm, right_margin - left_margin, 20*mm)
        y -= 35*mm

        # Draw a light gray line between questions
        c.setStrokeColor(lightgrey)
        c.setLineWidth(0.5)
        c.line(left_margin, y + 5*mm, right_margin, y + 5*mm)
        c.setStrokeColor(black)

    # Process each item in JSON data
    for index, (key, value) in enumerate(json_data.items(), 1):
        title = value.get('title', key)
        options = value.get('options', [])
        draw_text_with_options(index, title, options)
        field_counter += 1

    c.save()

# Load the JSON data
with open('data.json', 'r') as f:
    json_data = json.load(f)

# Create the PDF form
create_pdf_form(json_data, 'patient_form.pdf')

print("PDF form created successfully!")


```
