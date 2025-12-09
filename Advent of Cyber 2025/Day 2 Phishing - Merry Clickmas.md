# Phishing - Merry Clickmas

## Overview
- TBFC is performing authorized phishing assessments to evaluate employee cybersecurity awareness.
- Red team elves: Recon McRed, Exploit McRed, Pivot McRed.
- Goal: Test resistance to phishing & determine whether more training is needed.

## Key Concepts

### Social Engineering
- Human‑focused attack method using psychological manipulation.
- Common psychological triggers: urgency, curiosity, authority.
- Objective: trick targets into sharing info, clicking malicious links, or opening malicious files.

### Phishing
- Subset of social engineering using messages.
- Types:
  - Email phishing
  - Smishing (SMS)
  - Vishing (voice)
  - Quishing (QR)
  - Social media phishing
- TBFC teaches S.T.O.P. mnemonics:
  - **Suspicious? Telling me to click? Offering amazing deal? Pushing urgency?**
  - **Slow down, Type address manually, Open nothing unexpected, Prove the sender.**

## Fake Login Page (Phishing Trap)
- A fake TBFC login portal is pre‑built.
- Hosted using `./server.py` placed in `~/Rooms/AoC2025/Day02`.
- Running the script:
  ```
  ./server.py
  ```
- Server listens on `0.0.0.0:8000`.
- Visiting `http://CONNECTION_IP:8000` or `http://127.0.0.1:8000` displays the fake login page.
- Any submitted credentials appear directly in the terminal.

## Sending Phishing Email via Social‑Engineer Toolkit (SET)
- Launch SET:
  ```
  setoolkit
  ```
- Menu navigation:
  - `1` → Social‑Engineering Attacks  
  - `5` → Mass Mailer Attack  
  - `1` → Email a Single Address  

### Email Configuration Choices
- **Target email:** `factory@wareville.thm`
- **Email delivery:** Use open relay / own server
- **From address:** `updates@flyingdeer.thm`
- **From name:** `Flying Deer`
- **SMTP server:** `MACHINE_IP`
- **SMTP port:** 25 (default)
- **High priority?:** No
- **Attachments:** None
- **Subject:** “Shipping Schedule Changes”
- **Message format:** Plaintext
- **Body:** Must include the phishing URL `http://CONNECTION_IP:8000`

### Example Email Body
```
Dear elves,
Kindly note that shipping schedule changes have occurred due to increased orders.
Please confirm the new schedule by visiting http://CONNECTION_IP:8000
Best regards,
Flying Deer
END
```

## Results
- SET sends the phishing email.
- Credentials captured appear in the terminal running `server.py`.
- At least one set of **valid credentials** was obtained — a serious concern.
- Indicates TBFC may be vulnerable to real‑world phishing attacks.

## Key Takeaways
- Employees still fall for phishing traps.
- Awareness training must be reinforced.
- Monitoring logs recommended to check for real unauthorized access attempts.

