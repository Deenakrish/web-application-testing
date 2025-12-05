# web-application-testing
Comprehensive web application penetration testing using Burp suite &amp; OWASP Juice shop.Structured by OWASP Top 10 with dedicated branches.
# A01 – Broken Access Control: IDOR Test

This folder contains testing evidence for an IDOR vulnerability identified in the OWASP Juice Shop application.

## Contents
- **notes.md** – steps taken, request/response, conclusion  
- **request.txt** – raw HTTP request before tampering  
- **response.txt** – raw HTTP response after tampering  
- **/screenshots** – before & after screenshots  

## Finding Summary
The Feedback API allows modification of the `UserId` parameter, enabling users to impersonate others. This confirms an IDOR (Insecure Direct Object Reference) vulnerability.
