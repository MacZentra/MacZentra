# MacZentra

**A fast, native storage analyzer and cleaner for Mac.** See what is filling your disk, then clean it up safely. Everything you remove goes to the Trash, so you can always put it back.

[Website](https://maczentra.com/) · [Download](https://maczentra.com/) · [CLI reference](docs/MSC_CLI.md)

## Install

Download the disk image from [maczentra.com](https://maczentra.com/), or use Homebrew:

```bash
brew install --cask maczentra/tap/maczentra
```

MacZentra is signed and notarized by Apple, and it updates itself. Requires macOS Ventura (13) or later.

## What it does

- **Disk map:** scan your whole Mac, your home folder or any folder, and view it as a treemap, sunburst, tree table or sortable list of the largest items.
- **Insights:** one pass finds duplicates, stale files, caches, logs and large files, with a total of what you can safely reclaim.
- **Duplicates and similar images:** exact matches (BLAKE3) and near-identical photos, grouped by wasted space.
- **Developer junk:** Docker disk images, `node_modules`, Xcode DerivedData and archives, Python and Conda environments, Homebrew, Cargo and Gradle caches.
- **App uninstaller:** removes an app together with its leftovers, and finds orphaned files from apps you already deleted.
- **System monitor:** CPU, memory, network, battery and disk health (S.M.A.R.T.).
- **Privacy sweep:** history, cookies and caches for Safari, Chrome, Firefox, Brave, Edge, Arc and more.
- **Safety first:** a built-in guard refuses macOS system folders, and deletions use the Trash.

## Command line (Pro)

The `msc` command brings the same engine to the terminal. Install it from the app's Settings panel.

```bash
msc --help
msc scan --path ~/Downloads
msc duplicates --path ~/Pictures
msc large-files --threshold 500 --age 180
msc dev-junk --dry-run
msc dev-junk --apply
msc delete ~/Downloads/old-installer.dmg
msc diff --dry-run > cleanup-preview.patch
```

See the full list of 30 examples in [docs/MSC_CLI.md](docs/MSC_CLI.md).

## Verify the download

```bash
cd ~/Downloads
spctl --assess --type open --context context:primary-signature -v MacZentra_1.0.3_universal.dmg
```

You should see `accepted` and `source=Notarized Developer ID`.

## Links

- Website: <https://maczentra.com/>
- Homebrew tap: [MacZentra/homebrew-tap](https://github.com/MacZentra/homebrew-tap)
