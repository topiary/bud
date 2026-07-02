---
bud: 2 (TBD)
title: Grammars and Queries as Nickel Packages
author: "@mkatychev"
pr: -1
---

# Grammars and Queries as Nickel Packages

## Summary

https://nickel-lang.org/user-manual/package-management/

## Motivation

Decoupling

## Proposed design

```nickel
{
  name = "index",
  version = "1.0.0",
  authors = ["Me <me@example.com>"],
  minimal_nickel_version = "1.12.0",
  dependencies = {
    gh = 'Index { package = "github:topiary/topiary-rust", version = "1.0.0" }
  },
} | std.package.Manifest
```

### Infrastructure changes

publishing

https://github.com/nickel-lang/nickel-mine
