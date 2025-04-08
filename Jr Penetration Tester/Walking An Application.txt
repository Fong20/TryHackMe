
# Walking An Application

### Browser Tools Overview
- **View Source**: See raw HTML/CSS/JavaScript source code.
- **Inspector**: Live view of page elements; modify elements/styles.
- **Debugger**: Interact with and pause JavaScript execution.
- **Network**: View all HTTP requests made by the page.

---

### Manual Feature Discovery Example: Acme IT Support
| Feature | URL | Summary |
|--------|-----|---------|
| Home Page | `/` | Company overview with photo |
| Latest News | `/news` | List of articles, each linking to `/news/article?id=#` |
| News Article | `/news/article?id=1` | Individual articles; some restricted |
| Contact Page | `/contact` | Contact form with fields: name, email, message |
| Customers | `/customers` | Redirects to login |
| Customer Login | `/customers/login` | Login form |
| Customer Signup | `/customers/signup` | Signup form |
| Reset Password | `/customers/reset` | Password reset form |
| Dashboard | `/customers` | List of tickets, "Create Ticket" button |
| Create Ticket | `/customers/ticket/new` | Ticket form with textbox + file upload |
| Account | `/customers/account` | Edit account info |
| Logout | `/customers/logout` | Logs user out |

---

### Page Source Review Techniques
- **View Comments**: Look for `<!-- comments -->` for dev notes or links.
- **Find Hidden Links**: Look for `<a href="secret...">`.
- **Directory Listing**: Access shared dirs (e.g., `/assets`) to find sensitive files.
- **Identify Framework**: Comments or meta tags may reveal the framework and version (e.g., footer comment).
- **Use View Source**: Right-click → "View Page Source" or `view-source:URL`.

---

### Developer Tools Deep Dive

#### Inspector
- Use to:
  - View DOM elements live.
  - Bypass UI restrictions (e.g., paywalls).
- Example:
  - Inspect `.premium-customer-blocker`
  - Change `display: block` → `display: none` to bypass content block.

#### Debugger
- Purpose: Interact with JavaScript.
- Example:
  - On `/contact`, flash.min.js controls red popup.
  - Enable Pretty Print (`{}` icon) for formatting.
  - Find: `flash['remove']();`
  - Add breakpoint by clicking line number → refresh page → red popup remains visible (contains flag).

#### Network
- Purpose: Monitor HTTP traffic (XHR, AJAX).
- Steps:
  - Open Network tab → refresh page.
  - Submit contact form → observe AJAX request.
  - Click request → view POST data + destination → may reveal sensitive info or flag.
