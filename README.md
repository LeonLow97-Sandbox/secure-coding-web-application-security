# Contents

<ul>
    <li>Injection</li>
    <li>Broken Authentication</li>
    <li>Sensitive Data Exposure</li>
    <li>XML External Entities</li>
    <li>Broken Access Control</li>
    <li>Security Misconfiguration</li>
    <li>Cross-Site Scripting (XSS)</li>
    <li>Insecure Deserialization</li>
    <li>Using Components with Known Vulnerabilities</li>
    <li>Insufficient Logging and Monitoring</li>
</ul>

# OWASP Top 10 Web Application Security

### Injection

- What is it? Untrusted user input is interpreted by server and executed
- What is the impact? Data can be stolen, modified or deleted.
- How to prevent?
  - Reject untrusted/invalid input data
  - Use latest frameworks
  - Typically found by penetration testers / secure code review
  - Never trust user input / always sanitise user input

# Broken Authentication and Session Management

- What is it? Incorrectly build auth and session man. scheme that allows an attacher to impersonate another user.
- What is the impact? Attacker can take identify of victim.
- How to prevent?
  - Don't develop your own authentication schemes.
  - Use open source frameworks that are actively maintained by the community.
  - Use strong passwords (incl. upper, lower, number, special characters)
  - Require current credential when sensitive information is requested or changed.
  - Multi-factor authentication (e.g., sms, password, fingerprint, iris scan, etc.)
  - Log out or expire session after X amount of time
  - Be careful with 'remember me' functionality.

### Cross-Site Scripting (XSS)

- What is it? Untrusted user input is interpreted by browser and executed.
- What is the impact? Hijack user sessions, deface websites (redirect to another website), change content.
- How to prevent?
  - Escape untrusted input data / Untrusting user input data.
  - Latest UI framework

### Broken Access Control

- What is it? Restrictions on what authenticated users are allowed to do are not properly enforced. Improper enforcement of authorization.
- What is the impact? Attackers can assess data, view sensitive files and modify data.
- How to prevent?

  - Application should not solely rely on user input; check access rights on UI level and server level for requests to resources (e.g., data).
  - Deny access by default.

- E.g., Patient changes the URL from `www.hospital.com/patients/account/` to `www.hospital.com/doctor/account`

### Security Misconfiguration

- What is it? Human mistake of misconfigurating the system (e.g., providing a user with a default password).
- What is the impact? Depends on the misconfiguration. Worst misconfiguration could result in loss of the system.
- How to prevent?

  - Force change of default credentials
  - Least privilege: turn everything off by default (debugging, admin interface, etc.)
  - Static tools that scan code for default settings.
  - Keep pacthing, updating and testing the system
  - Regularly audit system deployment in production
  - Contunuously scan for vulneribilities, train your staff and focus on building & shipping more secure products.

- E.g., Connecting default webcam online with the default password. Other people can login online to your webcam.

### Sensitive Data Exposure

- What is it? Sensitive data is exposed, e.g., soaicl security numbers, passwords, health records.
- What is the impact? Data that are lost, exposed or corrupted can have severe impact on business continuity.
- How to prevent?

  - Always obscure data (credit card numbers are almost always obscured).
  - Update cryptographic algorithm (MD5, DES, SHA-0 and SHA-1 are insecure).
  - Use salted encryption on storage of passwords.

- What is the difference between encryption at rest and in transit?
  - Encryption at rest covers stored data, while encryption in transit covers data in flux (i.e. moving from one point to another point).
  - There are new developments that encrypt data in use (e.g., by processor). An example of this is Microsoft confidential compute.

### Insufficient Attack Protection

- What is it? Applications that are attacked but do not recognize it as an attack , letting the attacker attack again and again.
- What is the impact? Leak of data, decrease application availability.
- How to prevent? 
    - Detect and log normal and abnormal use of application
    - Respond by automatically blocking abnormal users or range of IP addresses.
    - Patch abnormal use quickly.

- Example:
    - In Frontend, someone uses program that logs on 100 times per minute
    - System then tries to process log attempts and fails
    - Another person can't log on because the system is unavailable.

### Cross-site request forgery (CSRF)

- What is it? An attack that force a victim to execute unwanted actions on a web application in which they are currently authenticated.
- What is the impact? Victim unknowingly executes transactions.
- How to prevent?
    - Reauthenticate for all critical actions (e.g., transfer money)
    - Include hidden token in request
    - Most web frameworks have built-in CRSF protection, but isn't enabled by default.

- Example:
    - User is logged on and is about to transfer funds over to an account with a legit URL as shown below:
    - `http://yourbank.com/transferFunds?amount=1000&desAccount=75218932487`
    - The attacker modifies the legit URL and embeds it into another website that is open in your browser on a different tab:
    - Attack: <img src=http://yourbank.com/transferFunds?amount=1000&desAccount=12222222223 />
    - The attacker hides the attack behind an image (img) and as soon as the victim clicks on the image, his funds will be transferred to account number 12222222223.

