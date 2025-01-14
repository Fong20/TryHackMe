
# Networking Core Protocols

## **Domain Name System (DNS)**
- **Purpose**: Maps domain names to IP addresses, eliminating the need to memorize IPs.
- **Layer**: Application Layer (Layer 7 of OSI model).
- **Ports**:
  - UDP port 53 (default)
  - TCP port 53 (fallback)
- **Common DNS Records**:
  - **A Record**: Maps hostname to IPv4 address (e.g., `example.com -> 172.17.2.172`).
  - **AAAA Record**: Maps hostname to IPv6 address.
  - **CNAME Record**: Maps one domain name to another (e.g., `www.example.com -> example.com`).
  - **MX Record**: Specifies mail server for a domain.

### **Tools for DNS Lookup**
- **nslookup**: Query DNS for records.
- **tshark**: Analyze DNS query packets (e.g., `tshark -r dns-query.pcapng`).

---

## **WHOIS Records**
- **Purpose**: Publicly available data on domain registrants (e.g., name, email, address).
- **Tools**: Command-line `whois` for domain lookup.
- **Privacy**: Can use services to hide personal info from WHOIS.

**Example of whois command in terminal**

![image](https://github.com/user-attachments/assets/11d27b2e-2757-428e-9bf3-3585d17b9aea)

---

## **HTTP and HTTPS**
- **Purpose**: Protocols for web communication.
- **Ports**:
  - HTTP: TCP port 80
  - HTTPS: TCP port 443
- **Common HTTP Methods**:
  - **GET**: Retrieve data (e.g., HTML or image).
  - **POST**: Submit new data (e.g., form submission).
  - **PUT**: Create/update resources.
  - **DELETE**: Delete specified resource.

**Example of HTTP messages sent between client and server recorded in Wireshark**

In the following example, Firefox browser was used to access the web server oeb page 10.10.41.192. The browser fetches the web page and displays it perfectly; however, we are interested in what happens behind the scenes.

Using Wireshark, we can examine the exchange between the Firefox browser and the web server more closely. The screenshot below from Wireshark shows the text sent by our browser in red and the web server response in blue. As you can tell, a lot of information is exchanged between the client and the server that does not get rendered to the user. Examples include the web server version and when the page was last modified.

![image](https://github.com/user-attachments/assets/fdc34aa7-29e3-41d4-b5a9-0f778ac92060)

---

## **File Transfer Protocol (FTP)**
- **Purpose**: Transfers files efficiently.
- **Ports**: 
  - Command: TCP port 21
  - Data Transfer: Separate connection.
- **Commands**:
  - `USER`: input username.
  - `PASS`: input password.
  - `RETR`: Download file from the FTP server to the client.
  - `STOR`: Upload file from client to FTP Server.

**Example of ftp command in terminal used to retreive files**

![image](https://github.com/user-attachments/assets/51b3bb49-c82c-4350-b07d-4991a601f8ec)

We used Wireshark to examine the exchanged messages more closely. The client’s messages are in red, while the server’s responses are in blue. Notice how various commands differ between the client and the server. For example, when you type ls on the client, the client sends LIST to the server. One last thing to note is that the directory listing and the file we downloaded are sent over a separate connection each.

![image](https://github.com/user-attachments/assets/fda8bda7-8abc-4457-83d9-95f16dc88a77)

---

## **Email Protocols**

### **SMTP (Simple Mail Transfer Protocol)**
- **Purpose**: Send emails from clients to servers or between servers.
- **Port**: TCP port 25 (default).
- **Commands**:
  - `HELO`/`EHLO`: Start SMTP session.
  - `MAIL FROM`: Specify sender's email address.
  - `RCPT TO`: Specify recipient's email address.
  - `DATA`: Begin sending email content.
  - `.`: sent on a line by itself to indicate the end of the email content.

**Example of smtp command in terminal used to send email**

The terminal below shows an example of an email sent via telnet. The SMTP server listens on TCP port 25 by default.

![image](https://github.com/user-attachments/assets/7e668209-ff64-430d-b091-7f48236f6b2e)

Obviously, sending an email using telnet is quite cumbersome; however, it helps you better understand the commands that your email client issues under the hood. The Wireshark capture shows the exchange in colours; the client’s messages are in red, while the server’s responses are in blue.

![image](https://github.com/user-attachments/assets/9f783978-80c5-4dc7-8190-e26b9e9320d5)

### **POP3 (Post Office Protocol v3)**
- **Purpose**: Retrieve emails from a server to a single client.
- **Port**: TCP port 110.
- **Commands**:
  - `USER`: identifies the username
  - `PASS`: provides user password.
  - `STAT`: Gets the number of messages and their size.
  - `LIST`: List down all the messages.
  - `RETR <msg number>`: Retrieve the message.
  - `DELE <msg number>`: Mark message for deletion.
  - `QUIT`: Ends POP3 session.

**Example of pop3 command in terminal used to retrieve email**

In the terminal below, we can see a POP3 session over telnet. Since the POP3 server listens on TCP port 110 by default, the command to connect to the TELNET port is telnet MACHINE_IP 110. The exchange below retrieves the email message sent in the previous task.

![image](https://github.com/user-attachments/assets/12efc362-9fc4-4a61-ac2a-feeaa1e0654e)

As per previous Wireshark captures, the commands in red are sent by the client, and the lines in blue are the server’s. It is also clear that someone capturing the traffic can read the passwords.

![image](https://github.com/user-attachments/assets/943393d2-1dc9-4c5c-9bbd-987194a0490a)

### **IMAP (Internet Message Access Protocol)**
- **Purpose**: Synchronize emails across multiple devices.
- **Port**: TCP port 143.
- **Commands**:
  - `LOGIN <username> <password>`: Authenticates user.
  - `SELECT <mailbox>`: selects the mailbox to work with.
  - `FETCH <mail number> <data item name>`: Retrieve message. Eg: fetch 3 body[] indicates that we want to fetch message number 3, header and body.
  - `MOVE <sequence set> <data item name>`: Move message to another mailbox.
  - `LOGOUT`: End session.

**Example of imap command in terminal used to retrieve email**

Knowing that the IMAP server listens on TCP port 143 by default, we will use telnet to connect to MACHINE_IP’s port 143 and fetch the message we sent in an earlier task.

![image](https://github.com/user-attachments/assets/e94d237b-ee43-4e54-aa83-29aaca005794)

The screenshot below shows the exchanged messages between the client and the server as seen from Wireshark. The client only needed to send four commands, shown in red, and the “long” server responses are shown in blue.

![image](https://github.com/user-attachments/assets/374b966c-1e9a-48f2-b2da-c5e396ab000f)

---

## **Comparison: POP3 vs. IMAP**
- **POP3**: Emails are downloaded and often deleted from the server (single device use).
- **IMAP**: Emails stay on the server, allowing synchronization across devices.

---

