# Lexical Analyzer & Parser for a Simple Programming Language

## Overview

This project implements a **Lexical Analyzer and Parser** in C++ for a simplified programming language. It reads a source program, tokenizes it, builds a **symbol table**, and parses statements to check for **syntax and type correctness**.

It supports **variable declarations, expressions, conditional statements (`if`), loops (`while`), and switch-case statements**.

---

## Features

* **Lexical Analysis**

  * Tokenizes the input source code into keywords, identifiers, numbers (integers and real numbers), operators, and delimiters.
  * Handles **comments** (`//`) and **whitespace**.
  * Supports a set of reserved keywords:

    * `int`, `real`, `bool`, `true`, `false`, `if`, `while`, `switch`, `case`, `public`, `private`.

* **Symbol Table Management**

  * Linked-list-based symbol table.
  * Tracks variable names, line numbers, types, and print status.
  * Detects new identifiers and assigns unique type codes.

* **Parser**

  * Recursive descent parser for syntax checking.
  * Supports:

    * Variable declarations
    * Assignment statements
    * Expressions (arithmetic, relational, logical)
    * Conditional statements (`if`)
    * Loops (`while`)
    * Switch-case statements
  * Performs **type checking** and reports **type mismatches**.

* **Error Handling**

  * Detects syntax errors.
  * Detects type mismatches in expressions and assignments.

* **Output**

  * Prints the **symbol table** at the end, showing variable names and types.

---

## Token Types

Defined in `lexer.h`:

```cpp
typedef enum {
    END_OF_FILE, INT, REAL, BOO, TR, FA, IF, WHILE, SWITCH, CASE,
    PUBLIC, PRIVATE, NUM, REALNUM, NOT, PLUS, MINUS, DIV, MULT,
    GTEQ, GREATER, LTEQ, LESS, NOTEQUAL, LPAREN, RPAREN, EQUAL,
    COLON, COMMA, SEMICOLON, LBRACE, RBRACE, ID, ERROR
} TokenType;
```

* **Keywords:** `INT`, `REAL`, `BOO`, `TR`, `FA`, `IF`, `WHILE`, `SWITCH`, `CASE`, `PUBLIC`, `PRIVATE`
* **Operators:** `PLUS`, `MINUS`, `MULT`, `DIV`, `NOT`, relational operators
* **Delimiters:** `LPAREN`, `RPAREN`, `COLON`, `COMMA`, `SEMICOLON`, `LBRACE`, `RBRACE`
* **Identifiers:** `ID`
* **Numbers:** `NUM` (integer), `REALNUM` (real)
* **Error Handling:** `ERROR`

---

## Project Structure

* **`lexer.h`** — Lexical Analyzer and token definitions, symbol table functions, and type management.
* **`inputbuf.h`** — Handles input reading and character buffering.
* **`main.cpp`** — Implements the parser, symbol table, program execution, and error handling.

**Key Classes and Functions:**

* `LexicalAnalyzer`

  * `GetToken()` — Returns the next token from input.
  * `UngetToken(Token)` — Pushes a token back for reprocessing.
  * `SkipSpace()` / `SkipComment()` — Handles spaces and comments.
  * `ScanIdOrKeyword()`, `ScanNumber()` — Token scanning utilities.

* `Token`

  * Holds `lexeme`, `token_type`, and `line_no`.
  * `Print()` — Prints token information.

* Symbol Table Functions

  * `addtoList(name, lineNo, type)` — Adds an identifier to the symbol table.
  * `SearchList(name)` — Searches for an identifier, returning its type.
  * `updateTypes(LHS, RHS)` — Updates types for type propagation.

* Parser Functions

  * `parse_program()`, `parse_vardecl()`, `parse_stmt()`, `parse_expression()`, `parse_ifstmt()`, `parse_whilestmt()`, `parse_switchstmt()`, etc.

---

## Compilation and Execution

1. **Compile the project:**

```bash
g++ main.cpp -o parser
```

2. **Run the parser on a source file:**

```bash
./parser < source_code.txt
```

3. **Output:**

* Prints syntax and type errors if found.
* Prints the symbol table showing variable names and types.

---

## Example Symbol Table Output

```text
x: int #
y: real #
flag: bool #
```

---

## Notes

* Type codes:

  * `1` → Integer
  * `2` → Real
  * `3` → Boolean
  * `>3` → User-defined identifiers
* Symbol table is implemented as a linked list for simplicity.
* Recursive descent parsing is used to check **syntax correctness** and **type consistency**.
* Code references **Rida Bazzi’s 2016 implementation** (do not share this file externally).

