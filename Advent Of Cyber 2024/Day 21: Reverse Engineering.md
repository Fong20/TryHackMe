
# AOC Day 21: Reverse Engineering 

## Learning Objectives
1. Understanding the structure of a binary file.
2. Differences between disassembly and decompiling.
3. Familiarity with multi-stage binaries.
4. Practical experience in reversing a multi-stage binary.

---

## Introduction to Reverse Engineering
- **Definition**: Reverse Engineering (RE) involves deconstructing an application to understand its function.
- **Use in Cyber Security**: Analyze malicious applications, identify indicators, and develop defensive measures.
- **Example**: *WannaCry ransomware* was stopped by registering a domain discovered through reverse engineering.

---

## Binaries
- **Definition**: Files compiled from source code into machine instructions.
- **Key Structures**:
  - **Code Section**: Contains CPU-executable instructions.
  - **Data Section**: Stores variables, resources, etc.
  - **Import/Export Tables**: References additional libraries for functionality.

---

## Disassembly vs. Decompiling
| **Comparison**       | **Disassembly**                                             | **Decompiling**                                          |
|-----------------------|------------------------------------------------------------|---------------------------------------------------------|
| **Readability**       | Requires assembly and low-level knowledge.                | High-level programming knowledge needed.                |
| **Level of Output**   | Exact machine instructions (assembly).                     | Approximate high-level code (e.g., C++, C#).            |
| **Difficulty**        | Higher due to complexity of assembly.                     | Lower due to high-level readability.                    |
| **Usefulness**        | Detailed binary behavior analysis.                        | Quick logical flow understanding.                       |

---

## Multi-Stage Binaries
- **Stages**:
  1. **Dropper**: Lightweight binary for OS enumeration; downloads the main payload.
  2. **Payload**: Performs malicious actions (e.g., ransomware encryption).
- **Benefits for Attackers**:
  - Evades detection by splitting attack actions.
  - Allows conditional execution based on specific triggers.

---

## Practical Walkthrough
### Tools Used:
1. **PEStudio**: Static analysis for information extraction without execution.
   - Useful Outputs: File SHA-256 hash, section hashes, suspicious strings.
2. **ILSpy**: Decompiles .NET binaries into C# for readable analysis.

### Example Binary Analysis: `demo.exe`
1. **File Details**:
   - **Extension**: `.exe` (Windows Executable).
   - **Language**: Compiled with .NET Framework (C#).
2. **PEStudio Analysis**:
   - Extract SHA-256 hash for identification.
   - Analyze `.text` section (executable code).
   - Review suspicious strings (URLs, function names).
3. **ILSpy Analysis**:
   - Decompiled main function for execution flow:
     ```csharp
     private static void Main(string[] args)
     {
         Console.WriteLine("Hello THM DEMO Binary");
         Thread.Sleep(5000);
         string address = "http://10.10.10.10/img/tryhackme_connect.png";
         string text = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "thm-demo.png");

         using (WebClient webClient = new WebClient())
         {
             try
             {
                 Console.WriteLine("Downloading file...");
                 webClient.DownloadFile(address, text);
                 Console.WriteLine("File downloaded to: " + text);
                 Process.Start(new ProcessStartInfo(text) { UseShellExecute = true });
                 Console.WriteLine("Image opened successfully.");
             }
             catch (Exception ex)
             {
                 Console.WriteLine("An error occurred: " + ex.Message);
             }
         }

         Console.WriteLine("Bye Bye leaving Demo Binary");
         Thread.Sleep(5000);
     }
     ```
   - **Actions Identified**:
     - Downloads a PNG file to the desktop.
     - Opens the downloaded file using the default image viewer.
   - **Execution Notes**: Run in a sandbox only to observe behavior.

---

## Task
- Reverse the application `WarevilleApp.exe` located in `C:\Users\Administrator\Desktop\`.
- Use PEStudio for static analysis and ILSpy for decompilation.

---
