# `msc` — MacZentra command-line companion (Pro)

`msc` (binary name `msc-cli`) is MacZentra's headless companion for the terminal. It runs the same scanner, duplicate finder and developer-junk engine as the desktop app. Every invocation checks for a valid Pro license; without one it prints "Upgrade Required" and exits non-zero. All deletions go to the macOS Trash and are recoverable.

Install it from the app's Settings panel. It links to `/usr/local/bin/msc`, or `~/.local/bin/msc` if that isn't writable.

## `msc --help`

```text
MacZentra — headless CLI (Pro)

USAGE
  msc <command> [options]

COMMANDS
  dev-junk [--dry-run] [--apply]
      Scan (and optionally clean) developer junk (Docker.raw, Node/Xcode/Python)
  scan [--path <dir>]
      Fast parallel disk-usage sweep of a directory
  duplicates [--path <dir>]
      Find exact-duplicate files under a directory
  large-files [--path <dir>] [--threshold <MB>] [--age <days>] [--apply]
      Find (and with --apply, delete) large/old files
  delete <path>...
      Move one or more paths to the Trash (recoverable)
  diff [--dry-run]
      Print the Git-style deletion preview to stdout
  help
      Show this help

All deletions move items to the macOS Trash (recoverable).
```

`msc help`, `msc -h`, `msc --help` and plain `msc` all print this.

## Examples

### Help
```bash
msc --help                                   # 1. full usage
msc -h                                       # 2. short flag
msc help                                     # 3. subcommand form
```

### Disk usage (`scan`)
```bash
msc scan                                     # 4. scan your home folder (default)
msc scan --path ~/Desktop                    # 5. one folder
msc scan --path ~/Library/Caches             # 6. what's in your caches
msc scan --path /Applications                # 7. installed apps
msc scan --path /Volumes/Backup              # 8. an external drive
msc scan --path ~/Downloads                  # 9. the usual suspect
```

### Duplicates (`duplicates`)
```bash
msc duplicates                               # 10. exact duplicates under home
msc duplicates --path ~/Pictures             # 11. photo duplicates
msc duplicates --path ~/Documents            # 12. documents
msc duplicates --path ~/Downloads            # 13. repeated downloads
```

### Large and old files (`large-files`)
```bash
msc large-files                              # 14. defaults, report only
msc large-files --threshold 100              # 15. files over 100 MB
msc large-files --threshold 1000             # 16. files over ~1 GB
msc large-files --age 365                    # 17. not touched in a year
msc large-files --path ~/Movies --threshold 500 --age 180   # 18. big, old movies
msc large-files --path ~/Downloads --threshold 50 --apply   # 19. move matches to Trash
```

### Developer junk (`dev-junk`)
```bash
msc dev-junk                                 # 20. scan Docker, Xcode, node_modules, Python
msc dev-junk --dry-run                       # 21. explicit preview, deletes nothing
msc dev-junk --apply                         # 22. clean the safe-by-default items
```
`--apply` only touches items marked safe by default. Risky ones (for example `Docker.raw`, orphaned modules, Conda envs, Archives) are never removed automatically.

### Delete (`delete`)
```bash
msc delete ~/Downloads/old-installer.dmg     # 23. one file to the Trash
msc delete ~/Downloads/a.zip ~/Downloads/b.zip   # 24. several paths
msc delete ~/Projects/old-app/node_modules   # 25. a folder
msc delete "$HOME/Desktop/Screen Recording.mov"  # 26. quote paths with spaces
```

### Preview and scripting (`diff`, pipes)
```bash
msc diff                                     # 27. Git-style deletion preview
msc diff --dry-run > cleanup-preview.patch   # 28. save the preview for review
msc scan --path ~/Library | less -R          # 29. page colored output
msc duplicates --path ~/Pictures > dupes.txt # 30. save a report
```

## Tips

- Colors turn off automatically when output isn't a terminal, so piping and redirecting give clean text.
- Review with `--dry-run` or `diff` before using `--apply` or `delete`.
- Items go to the Trash, so you can put anything back from Finder.
