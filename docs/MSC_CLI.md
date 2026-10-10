# `msc` — MacZentra command-line companion (Pro)

`msc` brings the same engine as the desktop app to the terminal. It needs a Pro license (`msc license status` checks it). All deletions go to the macOS Trash. Install it from the app's Settings panel. `msc --help` prints everything on this page.

## Commands

```text
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
  insights
      Full storage analysis: duplicates, stale files, caches, logs, large files
  junk [--dry-run] [--apply]
      Scan (and with --apply, clean) user caches, logs and old installers
  protect [list | add <dir> | remove <dir>]
      Manage folders every scan and cleanup skips
  license [status]
      Show whether a Pro license is active on this Mac
  help
      Show this help
```

## Examples

```text
  Help
   1. msc --help
   2. msc -h
   3. msc help

  Disk usage
   4. msc scan
   5. msc scan --path ~/Desktop
   6. msc scan --path ~/Library/Caches
   7. msc scan --path /Applications
   8. msc scan --path /Volumes/Backup
   9. msc scan --path ~/Downloads

  Duplicates
  10. msc duplicates
  11. msc duplicates --path ~/Pictures
  12. msc duplicates --path ~/Documents
  13. msc duplicates --path ~/Downloads

  Large and old files
  14. msc large-files
  15. msc large-files --threshold 100
  16. msc large-files --threshold 1000
  17. msc large-files --age 365
  18. msc large-files --path ~/Movies --threshold 500 --age 180
  19. msc large-files --path ~/Downloads --threshold 50 --apply

  Developer junk
  20. msc dev-junk
  21. msc dev-junk --dry-run
  22. msc dev-junk --apply

  Delete (moves to Trash)
  23. msc delete ~/Downloads/old-installer.dmg
  24. msc delete ~/Downloads/a.zip ~/Downloads/b.zip
  25. msc delete ~/Projects/old-app/node_modules
  26. msc delete "$HOME/Desktop/Screen Recording.mov"

  Preview and scripting
  27. msc diff
  28. msc diff --dry-run > cleanup-preview.patch
  29. msc scan --path ~/Library | less -R
  30. msc duplicates --path ~/Pictures > dupes.txt

MORE EXAMPLES
  (msc covers scan, duplicates, large files, developer junk, delete and diff.
   Treemap, uninstaller, snapshots, browser sweep and system monitor are
   desktop-app features and are not in the CLI.)

  Find what is eating space
  31. msc scan --path ~
  32. msc scan --path ~/Library/Developer
  33. msc scan --path ~/Library/Application\ Support
  34. msc scan --path ~/Library/Containers
  35. msc scan --path /Volumes/Photos
  36. msc scan --path ~/Movies | head -30

  Developer machines
  37. msc dev-junk --dry-run
  38. msc dev-junk --dry-run > before.txt
  39. msc dev-junk --apply
  40. msc scan --path ~/Projects
  41. msc delete ~/Projects/old/node_modules ~/Projects/old2/node_modules

  Photos, downloads and documents
  42. msc duplicates --path ~/Pictures/Imports
  43. msc duplicates --path ~/Downloads
  44. msc large-files --path ~/Downloads --threshold 200 --age 90
  45. msc large-files --path ~/Desktop --threshold 100
  46. msc large-files --path ~/Movies --threshold 1000 --age 365

  Safe cleanup workflow
  47. msc diff --dry-run
  48. msc diff --dry-run > preview.patch
  49. msc large-files --path ~/Downloads --threshold 50 --apply

  Automation
  50. msc scan --path ~ > ~/Desktop/disk-report-$(date +%F).txt
  51. alias cleanmac='msc dev-junk --dry-run && msc large-files --threshold 500'
  52. 0 9 * * 1 /usr/local/bin/msc duplicates --path ~/Downloads > ~/dupes.txt   (crontab line)
  53. msc scan --path ~ | grep -i "GB"
  54. msc duplicates --path ~/Documents | wc -l
  55. command -v msc || echo "msc not installed"

  New commands
  56. msc insights
  57. msc junk
  58. msc junk --apply
  59. msc protect list
  60. msc protect add ~/Documents/Taxes
  61. msc protect remove ~/Documents/Taxes
  62. msc license status
```
