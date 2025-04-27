
# Burp Suite Repeater

## Purpose & Functionality
- **Burp Suite Repeater** is used to **modify and resend intercepted requests**.
- Supports requests from **Burp Proxy** or **manual creation** (similar to cURL).
- Ideal for **manual exploration and endpoint testing**.
- Offers **graphical interface**, multiple views for requests/responses including rendering engine.

## Interface Overview
1. **Request List**: Top-left, manages multiple requests.
2. **Request Controls**: Below Request List; includes Send, Cancel, and History navigation.
3. **Request and Response View**: Center section, shows editable request and corresponding response.
4. **Layout Options**: Top-right of view section; layouts include side-by-side, vertical, or tabbed.
5. **Inspector**: Right-hand side; allows intuitive request editing.
6. **Target**: Above Inspector; shows destination IP/domain.

## Using Repeater
- Requests are often sent from **Proxy to Repeater** (Right-click > Send to Repeater or `Ctrl + R`).
- Requests appear in **Request View**, Target auto-filled.
- Click **Send** to populate the **Response View**.
- Modify requests in Request View and re-send for updated responses.
- Use **history buttons** to navigate modifications.

### Example: Modify Header
- Change header: `Connection: close` → `Connection: open`
- Server may respond with `Connection: keep-alive`.

## Response Display Options
Located above response box:
- **Pretty**: Default, formatted for readability.
- **Raw**: Unmodified server response.
- **Hex**: Byte-level view, good for binary data.
- **Render**: Browser-like rendering of response (less common use).

### Extra Display Features
- **Show non-printable characters (`\n`)**: Displays hidden characters like `\r\n`.

## Inspector Panel
- Found in both **Proxy** and **Repeater**, far-right panel.
- Provides **tabular breakdown** of requests and responses.

### Editable Request Components
- **Request Attributes**: URL, HTTP method, protocol (e.g., HTTP/1 → HTTP/2).
- **Query Parameters**: From URL (e.g., `?redirect=false`).
- **Body Parameters**: From POST data.
- **Cookies**: Modifiable list of cookies.
- **Headers**: Can add/edit/remove headers.

### View-only Response Component
- **Response Headers**: Visible post-response, cannot be edited.

## Summary
- Repeater is a key Burp Suite module for hands-on request analysis.
- Inspector enhances usability with editable sections and real-time raw view synchronization.
