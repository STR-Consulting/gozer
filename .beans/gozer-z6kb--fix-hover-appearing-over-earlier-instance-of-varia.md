---
# gozer-z6kb
title: Fix hover appearing over earlier instance of variable
status: completed
type: bug
priority: normal
created_at: 2026-01-19T02:12:11Z
updated_at: 2026-01-19T02:16:18Z
---

When hovering over a variable like .ErrorCount that appears multiple times on a line, the hover tooltip appears over the first instance instead of the one under the cursor. The bug is in lines 170-172 of internal/template/analyzer/analyzer_lsp.go which overwrites the correct cursor position range with the definition's range.