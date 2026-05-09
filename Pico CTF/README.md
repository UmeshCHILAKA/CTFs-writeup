# Pico CTF - writeup

[My profile](https://learn.cylabacademy.org/users/UmeshC)

## Riddle Registry
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://challenge-files.picoctf.net/c_saffron_estate/752a14d378d241efef396229bf41330061c1a0e73f7b3268a7e6db8d94fd4cd1/confidential.pdf) and uncover the flag within the metadata.

### Actions performed
Checked the file properties **- Did not help**

Checked by opening in Notepad++  **- Did not help**

Checked metadata online [Read PDF Metadata, View PDF Metadata Online | PDFYeah](https://www.pdfyeah.com/view-pdf-metadata/) in the pdf and found author to be 
cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9mOTQzMDBjNH0=

This looks like base64 encoding. Decode it using online tool.  [CyberChef](https://cyberchef.io/)

~~picoCTF{puzzl3d_m3tadata_f0und!_f94300c4}~~


## Log Hunt
Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag?Download the [logs](https://challenge-files.picoctf.net/c_saffron_estate/ce7c1c992c13f4c2498aeb507697ef67d4a8a87adec67cb2db0b8e491103e18d/server.log) and figure out the full flag from the fragments.

### Actions performed
Downloaded the log file and clearly flagpart is visible in text. This is split over multiple files
 
~~picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}~~



## Hidden in plainsight
You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag.Download the jpg image [here](https://challenge-files.picoctf.net/c_saffron_estate/5037bce9fb8a1d1975211489cedcdcd2e374d9e1837d7ce76dc3355ba5d71952/img.jpg).

### Actions performed
Checked the plain text -  **did not find anything useful**

Checked the exiftool online [Free Online EXIF Metadata Viewer & Extractor Tool - ExifMeta](https://exifmeta.com/), nothing spl except 

Comment	**c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9**

Use magic feature of https://cyberchef.io/ when do not know what to do 

c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9   => from base64 translates to    **steghide:cEF6endvcmQ=**

cEF6endvcmQ=          =>   from base64 translates to **pAzzword**

**steghide** is the cli tool to hide/show the steganographed content from image file

Command : **steghide extract -sf img.jpg -p pAzzword**

Extracts data to a file. 

~~picoCTF{h1dd3n_1n_1m4g3_656e4d79}~~
