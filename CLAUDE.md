# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

HTML linter written in Go. Validates HTML for accessibility, best practices, and common mistakes. Implements rules from html-validate.org.

## Guidelines

- Be concise
- Run `golangci-lint run --fix` after modifying Go code
- Run `go test ./...` after changes
- **NEVER commit without explicit user request**
- Use external test packages (`package foo_test`)

## Commands

```bash
go build ./...                        # Build
go test ./...                         # Test all
go test ./linter -run TestLintContent # Run single test
golangci-lint run                     # Lint
go install .                          # Install to $GOBIN
go-html-validate --help               # Usage
```

## Architecture

**Data flow:** `main.go` → `linter.Linter` → `parser.ParseFragment` → `rules.Rule.Check()` → `reporter.Reporter`

**Key types:**
- `parser.Document` - parsed HTML tree with `Walk(func(*Node) bool)` for traversal
- `parser.Node` - wraps `html.Node` with `HasAttr()`, `GetAttr()`, `TextContent()`, `IsElement()` helpers
- `rules.Rule` interface - `Name()`, `Description()`, `Check(*parser.Document) []Result`
- `rules.Result` - lint finding with `Rule`, `Message`, `Filename`, `Line`, `Col`, `Severity`

**Template handling:** The parser preprocesses Go template syntax (`{{...}}`) before parsing. Files starting with `{{define` are marked as template fragments.

## Adding Rules

1. Create `rules/rule_name.go` implementing `rules.Rule` interface
2. Add rule name constant to `rules/rule.go`
3. Register in `NewRegistry()` in `rules/rule.go`
4. Add tests in `linter/linter_*_test.go` (grouped by category: accessibility, validation, deprecated, etc.)
