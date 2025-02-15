# JavaScript Essentials

## Variables
- Variables store data values.
- Declared using `var`, `let`, or `const`.
  - `var`: Function-scoped.
  - `let` & `const`: Block-scoped.

## Data Types
- Strings, Numbers, Boolean, Null, Undefined, Objects (arrays, objects).

## Functions
- Functions encapsulate reusable code blocks.
```javascript
function PrintResult(rollNum) {
    alert("Username with roll number " + rollNum + " has passed the exam");
}
for (let i = 0; i < 100; i++) {
    PrintResult(rollNumbers[i]);
}
```

## Loops
- Used to execute code repeatedly (`for`, `while`, `do...while`).

## Request-Response Cycle
- Client requests data from a server; server responds with data.

## Internal JavaScript
- JS embedded directly in HTML using `<script>` tags.
```html
<script>
    let x = 5, y = 10;
    let result = x + y;
    document.getElementById("result").innerHTML = "The result is: " + result;
</script>
```

## External JavaScript
- JS stored in separate `.js` files and linked in HTML.
```html
<script src="script.js"></script>
```

## Checking for Internal/External JS
- Right-click → View Page Source.
- Internal JS: `<script>...</script>`.
- External JS: `<script src="file.js"></script>`.

## Dialog Functions
### Alert
```javascript
alert("Hello THM");
```
### Prompt
```javascript
name = prompt("What is your name?");
alert("Hello " + name);
```
### Confirm
```javascript
confirm("Do you want to proceed?");
```

## JavaScript Exploits
### Example of Malicious JS
```html
<script>
    for (let i = 0; i < 3; i++) {
        alert("Hacked");
    }
</script>
```

## Conditional Statements
- If-Else Example:
```javascript
age = prompt("What is your age");
if (age >= 18) {
    document.getElementById("message").innerHTML = "You are an adult.";
} else {
    document.getElementById("message").innerHTML = "You are a minor.";
}
```

## Minification & Obfuscation
- Minifying: Reducing file size by removing whitespace, comments.
- Obfuscating: Making code harder to read.
- Example of obfuscation:
```javascript
(function(_0x114713,_0x2246f2){var _0x51a830=_0x33bf,...
```

## Best Practices
- Avoid client-side validation only; always validate on the server.
- Use trusted JS libraries.
- Never hardcode secrets:
```javascript
// Bad Practice
const privateAPIKey = 'pk_TryHackMe-1337';
```
- Minify & obfuscate production code to enhance security.
