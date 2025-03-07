
# AOC Day 19: Game Hacking using Frida

## Overview
- **Learning Objectives:**
  - Interact with an executable's API.
  - Intercept and modify internal APIs using Frida.
  - Hack a game with the help of Frida.
- **Key Concepts:**
  - Game hacking involves reverse engineering, memory manipulation, and network knowledge.
  - Executables rely on libraries (e.g., `.so` files) for reusable code.
  - Frida is a tool for analyzing, modifying, and interacting with live applications by injecting JavaScript.

## Understanding Frida Hooks
- **Hooks:**
  - `onEnter`: Access parameters (`args`) before function execution.
  - `onLeave`: Access or modify return values (`retval`) after function execution.
- **Pointer Operations:**
  - Use `ptr(value)` to allocate and point to memory.
  - Access data using `.toInt32()` or `.readCString()` for integers and strings, respectively.

## Example: Intercepting `say_hello`
- **Objective:** Replace a function argument with `1337`.
- **Steps:**
  1. Run Frida to generate handlers:
     ```bash
     frida-trace ./main -i '*'
     ```
  2. Edit handler file (`libhello.so/say_hello.js`):
     ```javascript
     Interceptor.attach(Module.findExportByName(null, "say_hello"), {
         onEnter: function (args) {
             var originalArgument = args[0].toInt32();
             console.log("Original argument: " + originalArgument);
             args[0] = ptr(1337);
         }
     });
     ```
  3. Execute with Frida:
     ```bash
     frida-trace ./main -i 'say*'
     ```
  4. Output:
     ```
     Hello, 1337!
     Original argument: 1
     ```

## TryUnlockMe Game
- **Start Game:**
  ```bash
  cd /home/ubuntu/Desktop/TryUnlockMe && ./TryUnlockMe
  ```

### Level 1: OTP Hacking
- **Intercept OTP Function:**
  ```bash
  frida-trace ./TryUnlockMe -i 'libaocgame.so!*'
  ```
- **Edit `_Z7set_otpi.js`:**
  ```javascript
  defineHandler({
      onEnter(log, args, state) {
          log('_Z7set_otpi()');
          log("Parameter:" + args[0].toInt32());
      },
      onLeave(log, retval, state) {}
  });
  ```
- **Log Output Example:**
  ```
  Parameter: 611696
  ```
- Use the logged parameter as the OTP.

### Level 2: Purchasing Items
- **Intercept Purchase Validation:**
  ```bash
  frida-trace ./TryUnlockMe -i 'libaocgame.so!*'
  ```
- **Edit `_Z17validate_purchaseiii.js`:**
  ```javascript
  defineHandler({
      onEnter(log, args, state) {
          log('_Z17validate_purchaseiii()');
          args[1] = ptr(0); // Set price to 0
      },
      onLeave(log, retval, state) {}
  });
  ```
- **Log Output Example:**
  ```
  PARAMETER 1: 0x1
  PARAMETER 2: 0x5
  PARAMETER 3: 0x1
  ```

### Level 3: Biometrics Bypass
- **Intercept Biometrics Check:**
  ```bash
  frida-trace ./TryUnlockMe -i 'libaocgame.so!*'
  ```
- **Edit `_Z16check_biometricsPKc.js`:**
  ```javascript
  defineHandler({
      onEnter(log, args, state) {
          log('_Z16check_biometricsPKc()');
          log("PARAMETER:" + Memory.readCString(args[0]));
      },
      onLeave(log, retval, state) {
          retval.replace(ptr(1)); // Set return value to True
      }
  });
  ```
- **Log Example:**
  ```
  PARAMETER: 1trYRV2vJImp9QiGEreHNmJ8LUNMyfF0W4YxXYsqrcdy1JEDArUYbmguE1GDgUDA
  The return value is: 0x0
  ```

## Commands Summary
1. **Run Frida:**
   ```bash
   frida-trace ./executable -i '*'
   ```
2. **Modify Arguments:**
   ```javascript
   args[0] = ptr(newValue);
   ```
3. **Modify Return Values:**
   ```javascript
   retval.replace(ptr(newValue));
   ```
