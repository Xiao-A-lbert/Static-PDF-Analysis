# Static PDF Analysis

<h2>Description</h2>
In this static pdf analysis, I use my linux CLI to run phython pdf parsing and ole dumping scripts to analyze hidden macros and objects contained in three pdfs. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>Linux CLI</b>
- <b>Virustotal</b>
- <b>DidierStevensSuite pdfparser</b>
- <b>DidierStevensSuite oledump</b>
- <b>DidierStevensSuite pdfid</b>


<h2>Environments Used </h2>

- <b>Unbuntu</b> 

<h2>Description</h2>
In this dynamic attachment malware analysis, I used tools like Hybrid-Analysis and CVE research to analyze a malicious email attachment. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>Hybrid-Analysis</b>
- <b>Virustotal</b>


<h2>Environments Used </h2>

- <b>Unbuntu</b> 

<br />
<br />
Here is a pdf with a suspicious link in pdf viewer.

![1) macro imbedded pdf](https://github.com/user-attachments/assets/0edc0b7a-562f-4929-926d-7bc45b97b2e6)

<br />
<br />
Generating a sha256 and checking on virustotal shows 9 vendor flags. 

![2) virustotal 256 check](https://github.com/user-attachments/assets/af194b7d-68ec-4199-b45c-60141941d411)

<br />
<br />  
I used didierstevenssuite pdf-parser.py script to parse it.

![3) using didierstevenssuite pfd parser tool](https://github.com/user-attachments/assets/03262bf3-8920-4cb2-be2e-9f29dd7453df)

<br />
<br />
The python script parses a URI for a google script. 

![4) using the tool shows us the URI for the link](https://github.com/user-attachments/assets/2bc2b59d-c3a3-4177-b5d0-5f197a9c7573)

<br />
<br />
The URI shows 1 vendor flag as phishing.

![4) virustotal shows the link flagged as phishing](https://github.com/user-attachments/assets/7b27faf4-aa2e-4bc1-aebd-6c6dd113b373)

<br />
<br />
Here is another suspicious pdf in pdf viewer with the "statement" blurred out.

![6) example 2](https://github.com/user-attachments/assets/9982a5b2-92d5-4686-a206-97c7e8335633)

<br />
<br />
Using the same pdf-parsing script with a -s flag so search for "/URI" outputs the URI within the pdf. 

![7) running pdf parser suing s flag to search for uri](https://github.com/user-attachments/assets/50705440-8787-43bd-8331-8105e6499d17)

<br />
<br />
Running this URI in virustotal shows 2 vendor flags for phishing. 

![8) 2 vendorc flags](https://github.com/user-attachments/assets/9acbd041-11ec-4896-83bd-f7830623c7d8)
<br />
<br />
Let's say you do not want to open the pfd in pdf viewer incase it might be imbedded with macros, using pdfid.py script by DidierStevensSuite helps enumerate JS, JavaScript, OpenAction, and an EmbeddedFile within the PDF.

![9) using pdfid script to look for IOCs without viewing the pdf ](https://github.com/user-attachments/assets/ca3a0c8b-0509-4d42-a314-6a2980850259)

<br />
<br />
Again, running DidierStevensSuite pdf-parser | more helps show what's inside the pdf. 

![10) run pdfparser to parse the pdf](https://github.com/user-attachments/assets/18ee77ba-0850-4c24-b7f3-3a9082d1759b)

<br />
<br />
Scrolling down through the objects, we can see an embedded file in object 8 and a JavaScript action in object 9.

![11) obj 8 contains embedded file, obj 9 contains jscript](https://github.com/user-attachments/assets/b41fd1da-3d2b-4e85-974b-46f7d73a41c0)

<br />
<br />
Running pdf-parser with "--object 8 --filter --raw --dump eicar-dropper.doc" dumps out the raw filtered content into a file named eicar-dropper.doc. 

![12) extracting the 8th object into raw format and dumping into eicar file name](https://github.com/user-attachments/assets/a9fee9e1-23a6-4dac-84df-0aebf774169c)

<br />
<br />
Running a file command on eicar-dropper.doc shows its a composite document file.
Running oledump on this file shows 2 embedded macros. 

![13) using oledump script shows embedded macros in the file](https://github.com/user-attachments/assets/abe3c8d7-e072-4a61-8bc0-a117a1e54163)
<br />
<br />
