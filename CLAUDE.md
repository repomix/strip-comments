# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is `@repomix/strip-comments`, a fork of [strip-comments](https://github.com/jonschlinkert/strip-comments) maintained for use in the Repomix project. It strips line and/or block comments from strings, supporting JavaScript, CSS, HTML, Python, Ruby, and many other languages.

## Commands

```bash
# Run all tests
npm test

# Run tests with coverage
npm run cover
```

## Architecture

The library uses a parse-then-compile architecture:

- **index.js** - Main entry point exposing `strip()`, `strip.block()`, `strip.line()`, `strip.first()`, and `strip.parse()`
- **lib/parse.js** - Tokenizer that parses input strings into a CST (Concrete Syntax Tree) of nodes
- **lib/compile.js** - Compiles the CST back to a string with comments removed
- **lib/languages.js** - Language-specific regex patterns for comment detection (block open/close, line comments)
- **lib/Node.js** - Node class for CST representation

### Adding Language Support

To add a new language, define its comment patterns in `lib/languages.js`:

```js
exports.newlang = {
  BLOCK_OPEN_REGEX: /^\/\*/,
  BLOCK_CLOSE_REGEX: /^\*\//,
  LINE_REGEX: /^\/\/.*/
};
```

## Publishing

Publishing is done via GitHub Actions with OIDC trusted publisher (`.github/workflows/publish.yml`). Trigger manually from the Actions tab after configuring npm trusted publishing.
