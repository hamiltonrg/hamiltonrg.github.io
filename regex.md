# Regex Cheat Sheet

This page provides a quick reference for common regular expression patterns and
how to use them with either `grep` on Linux/WSL2 or `findstr` on Windows.

## Common Patterns

| Pattern | Description |
| ------- | ----------- |
| `^foo`  | Line starts with `foo` |
| `foo$`  | Line ends with `foo` |
| `[0-9]+` | One or more digits |
| `\.log$`| File name ends with `.log` |

## Linux and WSL2 (grep)

Use `grep -E` to enable extended regular expressions.

```bash
# lines starting with "foo"
grep -E '^foo' filename

# lines ending with "foo"
grep -E 'foo$' filename

# find digits in files
grep -E '[0-9]+' filename

# recursive search for log files mentioning error and timeout (ignore case)
grep -Ri 'error.*timeout' --include='*.log' /path/to/search
```

## Windows (findstr)

`findstr` uses the `/R` switch for regular expressions.

```cmd
REM lines starting with "foo"
findstr /R "^foo" filename

REM lines ending with "foo"
findstr /R "foo$" filename

REM find digits in files
findstr /R "[0-9][0-9]*" filename

REM recursive search in log files for error and timeout (case-insensitive)
findstr /S /I /R "error.*timeout" *.log
```
