# copyq-wastebin

CopyQ commands for sharing clipboard entries via a [Wastebin](https://github.com/matze/wastebin) instance.

Right-click any text item in CopyQ and share it as a paste — with optional expiry, password protection, or burn-after-reading.

## Features

- **Share** — upload with default expiry (2 days)
- **Share with expiry** — pick from 1 hour to 30 days
- **Share with password** — generates a random 20-char password
- **Share (burn after reading)** — deleted after first view
- **Share with password (burn after reading)** — both
- **Configure** — set your Wastebin URL and default expiry

After sharing, the paste URL (and password/burn notice if applicable) is copied to your clipboard, ready to paste.

## Requirements

- CopyQ **9.0+** (needs `NetworkRequest` support)
- A [Wastebin](https://github.com/matze/wastebin) instance (default: `https://bin.bloerg.net`)

## Install

### Option 1: GUI

1. Copy the contents of `wastebin-commands.ini` to your clipboard
2. Open CopyQ → press **F6** (Command dialog)
3. Click **Paste Commands**
4. Click **OK**

### Option 2: CLI

```bash
curl -s https://raw.githubusercontent.com/thereisnotime/copyq-wastebin/master/wastebin-commands.ini | \
  copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
```

### Option 3: Load from file

```bash
git clone https://github.com/thereisnotime/copyq-wastebin.git
cat copyq-wastebin/wastebin-commands.ini | \
  copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
```

## Configuration

On first use, if no URL is configured, you'll be prompted to enter one. You can also configure anytime via the right-click menu: **Wastebin → Configure...**

Settings are stored using CopyQ's `settings()` API under the `wastebin/` namespace.

## Update

Remove old commands first, then install the new version:

```bash
copyq eval 'var c = commands(); var keep = []; for (var i = 0; i < c.length; i++) { if (String(c[i].name).indexOf("Wastebin") < 0) keep.push(c[i]); } setCommands(keep);' && \
curl -s https://raw.githubusercontent.com/thereisnotime/copyq-wastebin/master/wastebin-commands.ini | \
  copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
```

Your configuration (URL, default expiry) is preserved since it's stored separately via `settings()`.

## Uninstall

### CLI

```bash
copyq eval 'var c = commands(); var keep = []; for (var i = 0; i < c.length; i++) { if (String(c[i].name).indexOf("Wastebin") < 0) keep.push(c[i]); } setCommands(keep);'
```

### GUI

Open CopyQ → **F6** → select and delete all commands starting with "Wastebin|".

## More CopyQ plugins

- [copyq-savefile](https://github.com/thereisnotime/copyq-savefile) — save clipboard items to timestamped files on disk
- [copyq-qrcode](https://github.com/thereisnotime/copyq-qrcode) — generate QR codes from clipboard text
