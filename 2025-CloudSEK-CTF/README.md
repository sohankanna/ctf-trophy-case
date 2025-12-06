## CloudSEK CTF 2025

*   **Format:** Jeopardy-style, Individual CTF
*   **Rank:** 13th out of ~1600 participants (Top 1%)
*   **Performance:** 100% clear rate on assigned tasks (Solved 4 out of 4 challenges attempted).
*   **Categories Covered:** Web Exploitation, Mobile Security, OSINT, Scripting.

### Personal Reflection
Achieving a 13th place finish in a field of over 1,600 participants (with ~500 active) was a significant milestone. My approach for this CTF was "quality over quantity"—I focused on maintaining a 100% accuracy rate for the challenges I attempted. I successfully cleared a diverse range of categories, moving from Mobile OSINT to Web Privilege Escalation and Python Automation. The challenges were realistic and required chaining multiple vulnerabilities rather than just firing standard payloads.

### Highlight: "Ticket" (Web / Mobile / OSINT)
The most satisfying solve was **Ticket**, a hybrid challenge that required pivoting between Mobile Security, OSINT, and Web Exploitation.

The challenge started with only an Android package name (`com.strikebank.netbanking`). Instead of decompiling an APK blindly, I leveraged **OSINT** by searching the package on **BeVigil** (a mobile security search engine). This revealed a generated security report containing hardcoded secrets in the `strings.xml` file, including valid credentials and an encoded JWT secret key.

Using these credentials, I accessed the web portal but had low privileges. I realized the application used JWTs for authorization. I took the encoded secret found via OSINT, decoded it, and used it to perform a **JWT Signature Forgery** attack. By modifying the payload to `role: admin` and re-signing the token with the recovered secret, I successfully escalated privileges and captured the flag. This challenge perfectly illustrated how a small information leak in a mobile app can lead to a full compromise of the web backend.

### My Contribution & Key Skills
I solved 4 challenges, covering Web, Scripting, and OSINT.

*   **Mobile & Web Hybrid:** In the "Ticket" challenge, I demonstrated the ability to connect disparate information sources—using public OSINT reports to find hardcoded secrets (`strings.xml`) and using them to exploit backend logic (JWT Forgery).
*   **Source Code Review (PHP):** For the **Triangle** challenge, I identified a Backup File Disclosure (`login.php.bak`), which revealed the source code. I spotted a PHP Type Juggling vulnerability (Loose Comparison `==` vs `===`) in the OTP verification logic, allowing me to bypass 2FA by sending boolean `true` via JSON instead of a string.
*   **Protocol Manipulation (XXE):** In **Bad Feedback**, I identified that the server accepted XML input despite the form appearing to be standard HTML. I changed the `Content-Type` header to `application/xml` and injected an XXE payload to exfiltrate the flag from the root directory.
*   **Automation:** For **Nitro Automation**, I wrote a Python script using `requests` and regex to interact with a hidden API. The task required fetching a string, reversing it, Base64 encoding it, and submitting it back within a strict timeout, which was impossible to do manually.

#### Key Takeaways
1.  **Reconnaissance is Everything:** The "Ticket" challenge proved that you don't always need to reverse engineer a binary if you can find the OSINT footprint (like BeVigil reports) left behind by developers.
2.  **Read the Source:** Finding the `.bak` files in "Triangle" reminded me that "black box" testing often fails where "white box" analysis succeeds. Seeing the code made the PHP Type Juggling vulnerability obvious.
3.  **Cross-Domain Skills:** The ability to understand Android resources (`strings.xml`) and apply that knowledge to Web (JWTs) gave me an edge in solving the hybrid challenges quickly.

### Assets
<img width="1449" height="807" alt="Screenshot 2025-12-06 113156" src="https://github.com/user-attachments/assets/8c829b96-cda4-4f69-ab8c-0ff63e93413a" />
<img width="1296" height="400" alt="Score over Time(2)" src="https://github.com/user-attachments/assets/2c6aa0c5-dd12-4f63-ad46-4ba5a6a410b6" />
<img width="1490" height="810" alt="Screenshot 2025-12-06 130104" src="https://github.com/user-attachments/assets/32559ab3-2d5f-4417-9a3a-74b1f7ad0d34" />
