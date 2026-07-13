---
bud: 2 (TBD)
title: "`topiary test` query tester"
author: "@mkatychev"
pr: 10
---

# Proposal for `topiary test`

## Summary

Introduce a `topiary test` subcommand that lets query authors verify
formatting behaviour by running Topiary over annotated test inputs and
comparing the result against expected output.

## Motivation

* There's value to having test cases be in one huge file for side effects.
* One should not have to recompile the `topiary` binary to test query changes for built-in languages
* external grammar repositories such as [topiary-nushell](https://github.com/blindFS/topiary-nushell) should have comparable DX to what is happening in topiary

## Proposed design

* initial aim to have queries organized with comment delimiters similar to [corpus tests](https://tree-sitter.github.io/tree-sitter/creating-parsers/5-writing-tests.html#writing-tests)
for [`tree-sitter test`](https://github.com/tree-sitter/tree-sitter/blob/master/crates/cli/src/test.rs)
* This doesn't establish a complete correlation whether a test query was successful but it will check to see if there was any difference in the before and after test doc for a particular query
  - this is different from `topiary coverage` because it would check if the string value changed when a particular query is run v.s. if a query found matches
* to handle something akin to [topiary-nushell's pattern](https://github.com/blindFS/topiary-nushell/tree/main/test) we can do something similar to nushell's [`parse`](https://www.nushell.sh/commands/docs/parse.html) command where ranges are defined using a template string for _input_ and _expected_:
  `topiary test --input "test/input_{case}.nu" --expected "test/expected_{case}.nu"`

### Mockup

```bash
# ./my_lang/test/test1.myl
:'
 1. use native language line comment start followed by 4 or more `=` signs to
 2. next line test name
 3. new line equivalent `=` sign comment as 1.
 4. add final line-break
'

# ==================
# return-statement
# ==================

ok() {
  yeet 1;
}

# ==================
# loop
# ==================

$one by-one {
  utter "the good die ${one}";
}
```


Test report could look like this in stdout:
```sh-session
$ topiary test --dir ./my_lang/test --query ./my_lang/query.scm

FAILURE(S):
- test1.myl
  * return-statement (L10-L##)
  * loop (L19-L##)
```

## Alternatives considered

Instead of comments, one could use [`query_name!`](https://topiary.tweag.io/book/reference/capture-names/general.html#query_name) but DX may be different.

## Drawbacks

Enumerating queries and test files is a many to many complexity but could be
an acceptable complexity for now since it will improve coverage over present state.

## Backwards compatibility

`topiary test` is a new subcommand and adds no changes to existing
Topiary behaviour, so there are no backwards-compatibility concerns.

## Testing strategy

The subcommand will be exercised against Topiary's existing language queries
as well as [external grammar repositories](https://github.com/blindFS/topiary-nushell).

## Documentation impact

The Topiary Book and the generated manpages will need a new section for `topiary test`.

## Unresolved questions

* Do we want to apply a specific naming schema for our tests?
* How do we group multiple tests?
