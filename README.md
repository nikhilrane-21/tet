INSTRUCTIONS TO RUN:

USAGE:

Python version: Python 3.10.7

Download tesseract exe from https://github.com/UB-Mannheim/tesseract/wiki.

Direct link for the tesseract binary : https://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-w64-setup-v5.2.0.20220712.exe

Install this exe in `C:\Program Files\Tesseract-OCR`

OR

To make tesseract work, put in the exact path of tesseract in `pytesseract.tesseract_cmd` in file `script_withoutdb.py` line no. 275.

Download `'cmake'` from https://cmake.org/download/  

Add the `C:\Program Files\CMake\bin` path to systems' environment variables path.


Download Poppler binary : https://blog.alivate.com.au/poppler-windows/

Extract the zip into `C:\Program Files`

Add the bin folder path to systems' environment variables path. example path : `C:\Program Files\poppler-x.x.x\bin`



Create the Virtual environment : `python -m venv env`
Enable Environment : `.\env\Scripts\activate`
Install all the required dependencies : `pip install -r requirements.txt`



.

.
1) Create a folder named Invoices_info

2) (A)
To run the code using Mongo localhost connection:
`python script.py --pdf pdf_name.pdf`
eg: `python script.py --pdf HPYUV372.pdf`

OR
 
2) (B) 
To run the code without Mongo localhost connection:
`python script_withoutdb.py --pdf pdf_name.pdf`
eg: `python script_withoutdb.py --pdf HPYUV372.pdf`

3) (A)
A window will open up, if the invoice template has not been added before. Select the desired rectangles by dragging with help of mouse and then press c on keyboard

Select boxes in the order:
1.Keyword
2.Date of Invoice
3.Invoice No.
4.Total Bill Amount
5.Buyer Details
6.Seller Details   

Finally the texts are extracted and the template is saved in relevant files/db.

OR 

3) (B)
If template of invoice matches with any template present in stored template files/db, then the relevant texts get extracted automatically.







APPROACH

Bounding Boxes: In this bounding boxes are selected for desired fields that re keyword, Date of Invoice, Invoice No. Total Bill Amount, Buyer Address and Seller Address in the same order. To select a bounding box, click on the left most corner and then hold the mouse button and drag till the rightmost bottom corner. Then release the mouse button.The x and y coordinates for the topleft and bottomright corners are stored in rhe database mapped with their keywords. The next time an invoice is fed into the system, it searches for the matching keyword and if it finds it then it uses the already stored x y coordinates to extract the r5quired fields. if the system is unable to match the keyword it, we have to onboard a new template for that invoice.

The keyword is matched in the following way, i. First for every document in the database we check that if in the rectangle bounded by the keyword coordinates eact same keyword is present, if yes the thenkeyword is found. ii. Otherwise every word of the pdf is checked against every keyword present in the database, if a word of the pdf matches with any of the leywords the the first line of the seller address is matched to confirm for the template. If found the that tempalte is considered, otherwise onboarding mode is set on.

