
# IDOR 

## What is IDOR?
- IDOR (Insecure Direct Object Reference) is a type of access control vulnerability.
- Occurs when user input is used to access objects (e.g., files, data) without proper validation to ensure ownership.

### Example Scenario
- URL: http://online-service.thm/profile?user_id=1305
- Changing the user_id to another value (e.g., 1000) exposes another user's data.
- Proper validation should ensure that the logged-in user owns the requested object.

## Types of ID Implementations

1. Encoded IDs
   - Often used to pass data via query strings, POST data, or cookies.
   - Most common: Base64 encoding (uses a-z, A-Z, 0-9, =).
   - Easily decodable:
     - Decode: https://www.base64decode.org/
     - Encode: https://www.base64encode.org/

2. Hashed IDs
   - Can use hashing algorithms like MD5.
   - Example: ID 123 → 202cb962ac59075b964b07152d234b70 (MD5).
   - Tools like https://crackstation.net/ can help reverse hashes.

3. Unpredictable IDs
   - Not easily guessed or detected.
   - Testing method: Create two accounts and swap IDs between them.
   - If one account accesses the other’s data, an IDOR is present.

## Finding IDOR Vulnerabilities
- Endpoints may not always be visible in the browser’s address bar.
- Vulnerabilities can be found in:
  - AJAX requests
  - JavaScript files
  - Hidden or legacy parameters
- Parameter Mining: Discover undocumented or hidden parameters (e.g., /user/details?user_id=123).
