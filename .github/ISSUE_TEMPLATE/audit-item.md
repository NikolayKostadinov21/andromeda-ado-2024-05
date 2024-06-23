---
name: Audit item
about: These are the audit items that end up in the report
title: "VFS Vulnerability"
labels: "Bug"
assignees: "Nikolay Kostadinov"
---

## Summary
The function `is_vfs_path` in the `addresses.rs` contract located in the directory `packages/std/src/amp/`
The virtual file system path could be potentially exploited to contain symbols that are incompatible with regular OS regex standarts.

## Vulnerability Detail
The test that's performed below is passing even though it has to fail since the path isn't valid.

## Impact
The exploit has a Medium impact on the Andromeda OS ecosystem as it's used in each directory path.

## Code Snippet
```
    #[test]
    fn test_is_valid_vfs_path() {
        let addr = AndrAddr("АСДco_______   '  `jnfig....@!@#$%%^&*()_//////\\\\asdasagsduysgfiasu1q2312873182763||||||||||home/user/app/component".to_string());
        assert!(addr.is_vfs_path());
    }
```

## Tool used
Unit testing and manual review

## Recommendation
Use proven regex pattern checks that are validating that the path will not be compromised. E.g. the regex path `^(.+)\/([^\/]+)$`.
