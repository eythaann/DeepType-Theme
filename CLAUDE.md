# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

DeepType Theme is a Visual Studio Code color theme extension inspired by natural elements (sea, sunsets, rivers, and forests). The theme provides syntax highlighting for multiple languages with a dark color palette centered around a `#16161b` background.

## Development Commands

**Test the extension:**
Press F5 in VSCode or use the "Extension" launch configuration from `.vscode/launch.json`. This opens a new VSCode window with the extension loaded.

**Package for distribution:**
```bash
vsce package
```

## Architecture

### Core Components

**Theme Definition:** `themes/Ts Theme-color-theme.json`
- Main color theme file following VSCode's color theme JSON schema
- Defines UI colors (`colors` object) for editor, sidebar, tabs, status bar, etc.
- Defines syntax highlighting (`tokenColors` array) using TextMate grammar scopes
- Color palette emphasizes blues (#428aff, #00b3d3), oranges (#c05921, #d8ab70), and accent colors for different token types

**Grammar Extension:** `grammars/powershell.json`
- Custom TextMate grammar for PowerShell syntax highlighting
- Extends VSCode's PowerShell support with custom scopes like `command.parameter`, `path`, `string.noquoted`
- Uses patterns and repository for tokenization rules

**Extension Manifest:** `package.json`
- Contributes theme via `contributes.themes` pointing to the theme JSON file
- Contributes grammar via `contributes.grammars` for PowerShell language
- Published as "deep-type-theme" by eythaann

### Color Scheme Logic

The theme organizes syntax colors by semantic meaning:
- **Keywords/Storage:** Teal (#0483a3) - `const`, `let`, `this`, `typeof`, `new`
- **Functions:** Blue (#428aff) - function names, method calls, `constructor`
- **Control Flow:** Orange-brown (#8C4A32) - `import`, `export`, `if`, `else` (bold styling)
- **Parameters/Tags:** Red (#de3846) - function parameters, JSX tags, type parameters
- **Properties:** Orange (#c05921) - object keys, enum members, JSX attributes
- **Variables:** Gold (#d8ab70) - variable references, object properties
- **Types:** Yellow (#f0ac22) - class names, interfaces, inherited classes
- **Primitive Types:** Dark yellow (#cc850b) - `string`, `number`, etc.
- **Strings:** Green (#5dce74)
- **Numbers:** Cyan (#00c3f3)
- **Comments/Punctuation:** Gray (#6d6d6d)

### Language Support

Officially supported languages (as listed in README):
- JavaScript/TypeScript
- PowerShell (with custom grammar)
- Bash
- HTML/CSS
- JSX/TSX
- JSON
- XML
- YAML

## Key Implementation Details

**Scope Targeting:** The theme uses precise TextMate scope selectors to target specific language constructs. For example:
- `meta.method.declaration storage.type` specifically targets the `constructor` keyword
- `meta.field.declaration meta.type.annotation storage.modifier` targets `extends` in type definitions
- `meta.object.member meta.object-literal.key` targets object property definitions

**PowerShell Grammar:** The custom PowerShell grammar in `grammars/powershell.json` includes unique patterns for:
- Command parameters (flags like `-Path`, `-Name`)
- Unquoted strings after parameters
- Path detection for file system paths
- Variable patterns with property access (`$var:property`)