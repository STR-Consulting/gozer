---
# gozer-4moj
title: Fix commit skill to always create releases on push
status: completed
type: bug
priority: normal
created_at: 2026-01-19T16:54:46Z
updated_at: 2026-01-19T16:55:58Z
---

When PUSH=true, the commit skill should always create a new release. If NEW_VERSION is not explicitly set, auto-bump the patch version (e.g., v0.6.0 -> v0.6.1).