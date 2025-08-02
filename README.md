# Resume Information Extraction using NLP

This project implements an NLP-based pipeline to automatically extract structured information such as Name, Skills, Degree, Institutions, and Work Experience from raw resumes in .txt or .pdf format using SpaCy's Named Entity Recognition (NER).

## 🚀 Features

- Preprocesses a JSON dataset of annotated resumes
- Converts annotations to SpaCy training format
- Trains a custom NER model from scratch using spacy.blank()
- Handles overlapping and misaligned entity spans
- Supports testing with custom .txt or .pdf resumes
- Regex-based extraction of Email, Phone, and LinkedIn profiles

## 🧠 Extracted Entities
- Name
- Skills
- Degree
- College Name
- Graduation Year
- Email
- Phone number
- LinkedIn

## 📂 Files
- NER.ipynb – Main notebook for loading data, training the model, and testing on new resumes
- Entity Recognition in Resumes.json – Annotated resume dataset
- Utilities to test with .pdf and .txt resume inputs

## 🛠️ Dependencies
```

spacy==3.x
pdfplumber
PyMuPDF (fitz)
re
random
```

## 📌 How to Run

1. Upload the annotated JSON dataset
2. Run the notebook NER.ipynb cell by cell
3. Train the custom NER model
4. Test the model using your own .txt or .pdf resumes

## 📥 Example: Testing a TXT Resume
```
with open("your_resume.txt", "r", encoding="utf-8") as f:
    resume_text = f.read()
doc = nlp(resume_text)
for ent in doc.ents:
print(f"{ent.label_:<25} ➤ {ent.text}")
```
## 📥 Example: Testing a PDF Resume
```
import pdfplumber
with pdfplumber.open("your_resume.pdf") as pdf:
resume_text = " ".join(page.extract_text() for page in pdf.pages)


doc = nlp(resume_text)
for ent in doc.ents:
print(f"{ent.label_:<25} ➤ {ent.text}")
```
## 🔍 Regex Post-processing
```
import re
email_match = re.search(r'[\w.-]+@[\w.-]+', resume_text)
phone_match = re.search(r'+91[-\s]?[0-9]{10}', resume_text)
linkedin_match = re.search(r'linkedin.com/[^\s]+', resume_text)


if email_match:
print(f"Email ➤ {email_match.group()}")
if phone_match:
print(f"Phone ➤ {phone_match.group()}")
if linkedin_match:
print(f"LinkedIn ➤ {linkedin_match.group()}")
```
## 📊 Sample Output
```
Name                     ➤ Rahul Verma
Email                    ➤ rahul.verma@gmail.com
Phone                    ➤ +91-9876543210
LinkedIn                 ➤ linkedin.com/in/rahul-verma
Degree                   ➤ M.Tech in Data Science
College Name             ➤ Indian Institute of Technology
Skills                   ➤ Machine Learning, Python, SQL
  
```

## 📸 Visual Output
## 1. Extracted Entities from Plain Text Resume
<img width="542" height="170" alt="image" src="https://github.com/user-attachments/assets/75f08253-8405-4c77-85e1-b9ce500265c8" />
## 2. Extracted Entities from PDF Resume
<img width="370" height="153" alt="image" src="https://github.com/user-attachments/assets/1d128a64-34ca-4671-a283-1ddbb6c54e8c" />

## 📌 Notes
Misaligned or overlapping entity spans are automatically skipped.
Ensure entity annotations are clean and whitespace-free.
Training accuracy depends heavily on dataset quality and coverage.

## 💡 Future Work
Improve span alignment and annotation quality
Fine-tune using pre-trained SpaCy pipelines
Integrate with Streamlit for resume upload and instant extraction

## ✅ Conclusion
This project successfully demonstrates how Natural Language Processing (NLP) can be applied to extract structured information from unstructured resumes. By training a custom SpaCy NER model, the system can identify important entities such as Name, Degree, Institution, Skills, and Work Experience. Additional regex logic helps capture key contact information like Email and LinkedIn with high accuracy.
