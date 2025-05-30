# CyberChef: The Basics

## What is CyberChef?
CyberChef is a web-based tool that provides various cyber operation tasks such as encoding, decoding, encryption, and data manipulation. It operates on "recipes"—a series of ordered operations.

## Learning Objectives
- Understand what CyberChef is
- Navigate the CyberChef interface
- Learn common operations
- Create and process recipes

## Interface Overview
CyberChef consists of four main areas:
1. **Operations Area** – Lists all available operations, categorized for easy access.
2. **Recipe Area** – Allows users to build and customize recipes.
3. **Input Area** – Where data is entered for processing.
4. **Output Area** – Displays processed data.

## Key CyberChef Operations
### Encoding & Decoding
| Operation       | Description                                      | Example |
|----------------|--------------------------------------------------|---------|
| From Morse Code | Decodes Morse Code into text                    | `- .... .-. . .- - ...` → `THREATS` |
| URL Encode     | Encodes special characters for URL compatibility | `https://tryhackme.com` → `https%3A%2F%2Ftryhackme%2Ecom` |
| To Base64      | Encodes data into Base64 format                  | `This is fun!` → `VGhpcyBpcyBmdW4h` |
| To Hex         | Converts text to hexadecimal                     | `Hello` → `48 65 6C 6C 6F` |
| To Decimal     | Converts text to decimal representation          | `A` → `65` |
| ROT13          | Caesar cipher shifting letters by 13 places      | `HELLO` → `URYYB` |

### Extractors
| Operation                | Description |
|--------------------------|-------------|
| Extract IP addresses     | Finds all IPv4/IPv6 addresses |
| Extract URLs             | Extracts valid URLs from input |
| Extract email addresses  | Finds all email addresses in text |

### Date & Time Operations
| Operation            | Description |
|----------------------|-------------|
| From UNIX Timestamp | Converts UNIX timestamp to human-readable format |
| To UNIX Timestamp   | Converts date to UNIX timestamp |

### Data Format Conversions
| Operation       | Description                                       | Example |
|---------------|-------------------------------------------------|---------|
| From Base64   | Decodes Base64 back into text                   | `V2VsY29tZQ==` → `Welcome` |
| URL Decode    | Decodes percent-encoded URLs                    | `%2Fhome%2F` → `/home/` |
| From Base85   | Converts Base85-encoded data to text            | `BOu!rD]j7BEbo7` → `hello world` |
| From Base58   | Converts Base58-encoded data to text            | `AXLU7qR` → `Thm58` |

## Thought Process When Using CyberChef
1. **Set a Clear Objective** – Define what you need to achieve.
2. **Provide Input Data** – Paste/upload the data to be processed.
3. **Choose Operations** – Identify relevant operations based on the data.
4. **Check Output** – Verify if the result matches expectations.

