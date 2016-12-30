---
layout: post
title:  "Use OpenSSL to Generate PFX"
date:   2016-09-15 00:00:00 -0500
categories: OpenSSL cURL pkcs12 PKCS#12 PFX
---
# Use OpenSSL to Generate PFX
Thursday, September 15, 2016
<br>by Brian Hooper
<br>[brian.hooper@copyleft.io][author-email]

---

### Quick Summary  
Sometimes there are cases when you have a separate private key and certificate pair (perhaps with an intermediate certificate or two) that need to be combined into a single file.  This merge can be performed on the command line using OpenSSL.

The OpenSSL pkcs12 command allows PKCS#12 files (sometimes referred to as PFX files) to be created and parsed.

<br>

### The Command

    openssl pkcs12 -export -in myCertificate.pem -inkey myPrivate.key -out myNewPFX.pfx

    # OPTIONS EXPLAINED

    # -in <filename>
    # specifies filename of the PKCS#12 file to be parsed.

    # -inkey <filename>
    # Specifies the file to read the private key from.
    # If not present then a private key must be present in the input file.

    # -out <filename>
    # Specifies the filename to write certificates and private keys to.  
    # They are PEM format by default.

    # Although there are a large number of options most of them are very rarely used.  
    # See the Man Page for more.


<br>

### Using our new PFX

Let's say you ever need to test an external facing REST API over HTTPS that is secured via a Client SSL Certificates... you know, just to validate a renewed Client SSL Certificate before you ship it over to the client. ;)

The cURL command below will allow you to use your new .pfx file to authenticate and resolve the service via Public IP.  Simply change out the <parameters> for your test.  

    curl -H "Content-Type: application/json" -X GET -v --cert "<myNew.pfx:pa55word>" <https://rest.api.com/12345> --resolve <rest.api.com>:443:<ipaddress> --tlsv1.2

    # Note: When you create the PFX you will be prompted to create a password.
    # In this example our password is 'pa55word'


<br>
Cheers!
<br>-Brian





[author-email]: mailto:brian.hooper@copyleft.io
[email]: mailto:hello@copyleft.io
[twitter]: https://twitter.com/copyleftio
