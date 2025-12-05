
# IDOR (Insecure Direct Object Reference) Test

## 1. What Was Tested
Testing for IDOR in the OWASP Juice Shop Feedback API.  
Goal: Check whether a user can modify the `UserId` field and submit feedback on behalf of another user.

---

## 2. Steps Performed
1. Started Burp Suite and enabled Proxy.
2. Enabled FoxyProxy with `127.0.0.1:8080`.
3. Opened Juice Shop running at `http://127.0.0.1:3000/`.
4. Navigated to **Feedback** page and submitted a normal feedback.
5. Burp Suite captured the POST request to `/api/Feedbacks/`.
6. Sent the request to **Repeater**.
7. Modified the JSON body → changed `"UserId": 16` to `"UserId": 14`.
8. Sent the modified request.
9. Juice Shop responded with **success**, accepting the tampered User ID.

---

