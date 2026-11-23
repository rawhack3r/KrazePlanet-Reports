## Stored XSS Leading to Admin Account Takeover and Potential Mass Account Takeover

**Severity:** Critical  
**Affected Asset:** `https://forum.pwnedbox.site/`  

## 1. Vulnerability Description

A Stored Cross-Site Scripting (XSS) vulnerability was identified in the application. The application improperly handles user-supplied input in the parameter, allowing injected JavaScript to be stored on the server and executed in the browsers of users who subsequently access the affected content.

Unlike Reflected XSS, this vulnerability does not require the victim to click a specially crafted link every time. Once the malicious input is stored, the payload can execute whenever the affected content is retrieved and rendered.

## 2. Steps to Reproduce

1. Navigate to the affected application url.

```html
https://forum.pwnedbox.site/
```
2. Locate the functionality that accepts user-controlled input.
3. Submit the following proof-of-concept payload:

```html
"><img src=x onerror=alert(7)>
```

4. Save or submit the input.
5. Navigate to the affected page or reload the stored content.
6. Observe that JavaScript executes in the browser.

**Affected Parameter:** `post_id`

## 3. Proof of Concept (PoC) & Evidence


**1. Screenshots:**  
<img width="1916" height="872" alt="Screenshot 2026-11-23 075550" src="https://github.com/user-attachments/assets/3c400cd2-4c97-4acd-99b0-7242ffbb176e" />
<img width="1897" height="490" alt="Screenshot 2026-11-23 075523" src="https://github.com/user-attachments/assets/d5cbf6f8-2711-44c4-994a-2686a75c234c" />



**2. Video PoC:**  [https://drive.google.com/file/d/1n38vVkmTRjn7rxRs24OyhUbuvu_coHSb/view?usp=sharing]



The attached evidence demonstrates successful JavaScript execution, persistence of the injected payload, and the potential security impact of the vulnerability.

## 4. Security Impact

An attacker could exploit this vulnerability to:

- The stored XSS payload executes within an administrator's dashboard, it could compromise an administrator's authenticated session, enable unauthorized administrative actions, and lead to full administrative account takeover, depending on the application's security controls.
- Stored XSS may allow attackers to access sensitive information exposed through document.cookie and achieve account takeover if session cookies are accessible to JavaScript and other security protections do not prevent it.
- If the vulnerable parameter or functionality is publicly accessible, the issue could enable widespread exploitation and lead to mass account takeover affecting multiple users who access the compromised content.
- Execute arbitrary JavaScript in the security context of the affected website.
- Perform unauthorized actions through the victim's authenticated session, depending on application protections.
- Access sensitive information exposed to JavaScript within the page context.
- Target multiple users who access the affected stored content.

The impact may extend to administrators if they access the affected content, increasing the severity of the vulnerability.

## 5. Remediation

The following security measures are recommended:

1. **Context-Aware Output Encoding:** Properly encode all user-controlled data before rendering it in HTML, JavaScript, attributes, or other output contexts.
2. **Input Validation:** Validate incoming data against the expected format and permitted characters.
3. **HTML Sanitization:** If HTML input is required, use a reputable HTML sanitization library with a strict allowlist. Encode HTML special characters (&, <, >, ", ') into their respective HTML entities (&amp;, &lt;, &gt;, &quot;, &#x27;) before rendering user-controlled input to prevent JavaScript execution.
4. **Content Security Policy (CSP):** Implement a restrictive CSP to reduce the impact of successful XSS exploitation.
5. **Review Existing Stored Content:** Identify and remove previously stored malicious content.

## 6. References

- https://owasp.org/www-community/attacks/xss/
- https://owasp.org/www-project-web-security-testing-guide/
- https://cwe.mitre.org/data/definitions/79.html
