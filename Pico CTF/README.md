# Pico CTF - writeup
Writeups for Pico CTF

## Riddle Registry
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://https://challenge-files.picoctf.net/c_saffron_estate/752a14d378d241efef396229bf41330061c1a0e73f7b3268a7e6db8d94fd4cd1/confidential.pdf) and uncover the flag within the metadata.

### Actions performed
Checked the file properties **- Did not help**

Checked by opening in Notepad++  **- Did not help**

Checked metadata online [Read PDF Metadata, View PDF Metadata Online | PDFYeah](https://www.pdfyeah.com/view-pdf-metadata/) in the pdf and found author to be 
cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9mOTQzMDBjNH0=

This looks like base64 encoding. Decode it using online tool.  [CyberChef](https://cyberchef.io/)

~~picoCTF{puzzl3d_m3tadata_f0und!_f94300c4}~~
