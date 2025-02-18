# Burp Suite: The Basics

## Key Features

### 1. Proxy
- Intercepts and modifies requests and responses.
- Allows control over web traffic.

### 2. Repeater
- Captures, modifies, and resends requests.
- Useful for testing vulnerabilities like SQL Injection.

### 3. Intruder
- Limited in the Community edition but supports brute-force attacks and fuzzing.

### 4. Decoder
- Encodes and decodes payloads for data transformation.

### 5. Comparer
- Compares two pieces of data at word or byte level.

### 6. Sequencer
- Analyzes randomness in tokens like session cookies.

## Extending Burp Suite
- Supports extensions in **Java, Python (Jython), and Ruby (JRuby)**.
- **Burp Suite Extender** allows loading custom extensions.
- **BApp Store** provides third-party modules (some require a professional license).
- Example: **Logger++** extends logging capabilities.

---

## Setting Up Burp Suite Community

### 1. Initial Setup
- Accept terms and conditions.
- Default configuration is recommended.
- Training materials are available on the first launch.

### 2. Burp Dashboard Overview
Divided into four quadrants:
1. **Tasks** - Defines background tasks (e.g., Live Passive Crawl).
2. **Event Log** - Displays system actions and connection details.
3. **Issue Activity** (Professional only) - Lists detected vulnerabilities.
4. **Advisory** - Provides information on vulnerabilities.

### 3. Navigation & Modules
- **Top Menu Bar**: Allows switching between modules.
- **Sub-tabs**: Access module-specific settings.
- **Detaching Tabs**: Tabs can be detached into separate windows for better multitasking.
- **Keyboard Shortcuts**:
  - `Ctrl + Shift + D` → Dashboard
  - `Ctrl + Shift + T` → Target tab
  - `Ctrl + Shift + P` → Proxy tab
  - `Ctrl + Shift + I` → Intruder tab
  - `Ctrl + Shift + R` → Repeater tab

---

## Configuring Burp Suite

### 1. Settings
- **Global Settings**: Affect the entire Burp Suite installation.
- **Project Settings**: Specific to the current session (not saved in Community edition).

### 2. Accessing Settings
- Click the **Settings button** in the navigation bar.
- Categories include:
  - **Search**: Find specific settings.
  - **User Settings**: Global settings.
  - **Project Settings**: Session-based settings.
  - **Proxy Settings**: Quick access for proxy configurations.

---

## Burp Proxy - Key Concepts

### 1. Intercepting Requests
- Requests are held before reaching the server.
- Can be modified, forwarded, or dropped.
- Click **"Intercept is on"** to disable interception.

### 2. Logging & Analysis
- Requests are logged even if interception is off.
- **WebSockets** communication is also logged.
- Access logs via **HTTP history & WebSockets history**.

### 3. Proxy Settings
- **Response Interception**: Configure specific rules for intercepting responses.
- **Match & Replace**: Use regex to modify requests dynamically.

---

## Setting Up Proxy in Firefox utilizing FoxyProxy

### 1. Install FoxyProxy
- Already pre-installed in AttackBox.
- Click on the FoxyProxy button in Firefox.

### 2. Configure Burp Proxy
- **Title**: Burp
- **Proxy IP**: `127.0.0.1`
- **Port**: `8080`
- Save and activate the configuration.

### 3. Test the Proxy
- Open Burp Suite.
- Enable **Intercept** in the Proxy tab.
- Visit a webpage; the request should be intercepted.

---

## Target Tab Features

### 1. Site Map
- Displays visited pages.
- Useful for **mapping APIs and web applications**.

### 2. Issue Definitions
- Lists vulnerabilities that Burp Suite Professional scans for.
- Can be used for manual testing reference.

### 3. Scope Settings
- Defines which traffic is captured.
- Set scope by **right-clicking a target** and selecting **Add to Scope**.

---

## Burp Browser
- A built-in **Chromium-based** browser.
- Pre-configured for proxy use.
- Start via **Open Browser** in the Proxy tab.

### Running Burp Browser as Root (Linux)
- **Option 1 (Recommended)**: Create a low-privilege user.
- **Option 2 (Easier)**: Enable **Allow Burp's browser to run without a sandbox** in settings.

---

## Scoping & Filtering Traffic

### 1. Define Target Scope
- Right-click a target in **Target tab** → **Add to Scope**.
- Choose to **stop logging out-of-scope traffic**.

### 2. Filtering Proxy Traffic
- Go to **Proxy settings** → Enable **And URL is in target scope**.
- Ensures only scoped traffic is intercepted.

---

## Handling TLS/SSL Errors

### 1. Install Burp CA Certificate
- Navigate to `http://burp/cert` in Firefox.
- Save the `cacert.der` file.

### 2. Add Certificate to Firefox
- Open **Firefox settings** (`about:preferences`).
- Search for **Certificates** → Click **View Certificates**.
- Import `cacert.der` and check **Trust this CA to identify websites**.

Now Burp Suite will work with HTTPS sites without issues.


## Real World Example: XSS Testing

### 1. Testing for XSS
- Navigate to the **support form** at `http://10.10.223.225/ticket/`.
- XSS (Cross-Site Scripting) involves injecting **client-side scripts (JavaScript)** into a webpage.
- The **Reflected XSS** type only affects the user making the request.

### 2. Attempting the Attack
- Enter the following payload in the **Contact Email** field:
  ```html
  <script>alert("Succ3ssful XSS")</script>
  ```
- A **client-side filter** blocks the input, restricting special characters.

### 3. Bypassing the Client-Side Filter
- Use Burp Suite to intercept and modify the request:
  1. **Activate Burp Proxy** and enable **Intercept**.
  2. Fill in the form with:
     - **Email**: `pentester@example.thm`
     - **Query**: `"Test Attack"`
  3. **Submit the form** (Burp intercepts the request).
  4. Modify the **email field** in the intercepted request to:
     ```html
     <script>alert("Succ3ssful XSS")</script>
     ```
  5. **URL encode** the payload using `Ctrl + U`.
  6. **Forward the request**.

### 4. Confirmation of XSS
- A **JavaScript alert box** should pop up, confirming a successful XSS attack.
