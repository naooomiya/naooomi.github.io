---
title: 'ASCII, ANSI and Unicode'
date: 2019-11-25 17:48:33
tags: 
    - ASCII
    - ANSI
    - Unicode
    - UTF
categories: 
    - Encoding
---

### Character Encoding
A character encoding tells the computer how to interpret raw zeroes and ones into real characters. It usually does this by pairing numbers with characters. Words and sentences in text are created from characters and these characters are grouped into a character set. There are many different types of character encodings floating arounds at present, but the ones we deal most frequently with are ASCII, **8-bit** encodings, and Unicode-based encodings.

<!-- more -->

### ASCII
**American Standard Code for Information Interchange(ASCII)** is a character-encoding scheme and it was the first character encoding standard. It is a code for representing English characters as numbers, with each letter assigned a number from 0-127. Most modern character-encoding schemes are based on ASCII, though they support many additional characters. It is a single byte encoding only using the bottom **7 bits**. In an ASCII file, each alphabetic, numeric, or special character is represented with a **7-bit** binay number. 

### ANSI
- ANSI(American National Standards Institute) codes are standardized numeric or alphabetic codes issued by the American National Standards Institute to ensure uniform identification. 
- This is essentially an extension of the ASCII character set in that it includes all the ASCII characters with an additional 128 character codes. 
- ASCII just defines a 7 bit code page with 128 symbols. **ANSI** extends this to **8 bit** and there are serveral different code page for the symbols 128 to 255. It can only represent a maximum of 256 characters. 
- ANSI is very old and is used by OS like Windows 95/98 and older. 

### Unicode
- Unicode is a newer encoding which defines the internal text coding system in almost all OS used in computers at present, whether it is Windows, Unix, Macintosh, Linux or whatever, because Unicode can handle characters for almost all modern languages and even some ancient languages at the same time, as long as the client has fonts for the particular language installed in his system.
- Unicode uses a maximum of **32 bits** for each code point
	

### UTF
Unicode assigns each character a unique number, or code point. It defines two mapping methods, the **UTF(Unicode Transformation Format) encodings**, and the **UCS(Universal Character Set)** encodings. Unicode-based encodings implement the Unicode standard and include **UTF-8**, **UTF-16** and **UTF-32/UCS-4**. They go beyond **8-bits** and support almost every language in the world. UTF-8 is gaining traction as the dominant international encoding of the web. UTF-8, UTF-16 and UTF-32 are probably the most commonly used encodings.

#### UTF-8
- Uses **1 byte** to represesnt characters in the ASCII set, **two bytes** for characters in several more alphabetic blocks, and **three bytes** for the rest of the BMP. Supplementary characters use **4 bytes**. 
- UTF-8 uses a **multibyte encoding scheme** makes it possible to accommodate all these code point yet manages to consume minimal memory. The first byte of UTF-8 matches ASCII exactly, hence the most common characters only need a single byte. 

#### UTF-16
Uses **2 bytes** for any character in the BMP, and 4 bytes for supplementary characters.

#### UTF-32
Uses **4 bytes** for all characters. 

