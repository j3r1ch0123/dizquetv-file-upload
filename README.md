# dizqueTV File Upload to XSS Exploit

## Overview
This exploit targets a file upload vulnerability in **dizqueTV** versions 1.5.3-1.5.5. Due to insufficient sanitization in the file upload API, an attacker can upload arbitrary files, enabling potential **Cross-Site Scripting (XSS)** attacks. This exploit leverages the vulnerability to upload a crafted HTML file with embedded JavaScript.

**Exploit Author**: J3rich0123  
**Tested on**: Linux  
**Vendor**: [dizqueTV GitHub Repository](https://github.com/vexorian/dizquetv)  
**Version**: 1.5.3-1.5.5 (Required)  
**CVE**: N/A

## Vulnerable Component
The vulnerability resides in the file upload endpoint at `/api/upload/image`, which does not sanitize file contents or enforce strict file type restrictions. This allows the upload of files containing malicious code.

## Exploit Details
The exploit script creates and uploads an HTML file with a JavaScript-based XSS payload. Once uploaded, this payload can trigger on pages that render the file, potentially allowing the attacker to perform actions like cookie theft or redirection.

## Usage
### Prerequisites
- Python 3.x
- `requests` library

To install the required library:
```bash
pip install requests
```

Exploit Execution

Clone this repository.

Execute the exploit with the target URL as an argument:

```bash
python exploit.py <target_url>
```

Example usage:

```bash
python exploit.py http://localhost:8000/api/upload/image
```

Upon success, you’ll see confirmation messages indicating the file upload was successful.

Note: If the file renders in a browser with JavaScript enabled, the XSS alert will be triggered.

Example Output
plaintext

Reading malicious file: xss.html
Uploading malicious file: xss.html
Exploit successful! Attempted to upload: xss.html
Server response: (Server response message here)
PoC HTML Payload
The xss.html payload file created by this exploit contains:

html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>XSS Payload</title>
    <script>alert("Hacked!!!");</script>
</head>
<body>
    <h1>Testing XSS Payload</h1>
    <p>If the alert shows, the XSS attack was successful!</p>
</body>
</html>
```
Remediation
This vulnerability has been reported to the vendor, and a patch will be released in the next version. The patch will address file type sanitization and restrictions.

Disclaimer
This exploit is intended for educational and ethical purposes only. Unauthorized use of this exploit may violate laws and regulations. Use it responsibly.

