# Contributing

Thanks for considering a contribution! This is a small project so the process is lightweight.

## Reporting Issues

Open an issue on GitHub with:
- Your CopyQ version (`copyq --version`)
- What you expected vs what happened
- Any error output from running `copyq` in a terminal

## Submitting Changes

1. Fork the repo and create a branch
2. Make your changes to `wastebin-commands.ini`
3. Test by importing the commands into CopyQ:
   ```bash
   # Remove old commands
   copyq eval 'var c = commands(); var keep = []; for (var i = 0; i < c.length; i++) { if (String(c[i].name).indexOf("Wastebin") < 0) keep.push(c[i]); } setCommands(keep);'

   # Import your version
   cat wastebin-commands.ini | copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
   ```
4. Verify all submenu items work (share, expiry, password, burn, configure)
5. Open a PR with a short description of what you changed and why

## Things to Keep in Mind

- CopyQ 9.0+ is the minimum supported version (needs `NetworkRequest`)
- The commands use `settings()` for config persistence — don't break existing user settings
- Test with at least one public Wastebin instance (e.g. `https://bin.bloerg.net`)
- Keep the INI format compatible with `importCommands()` — use the `[Commands]` format with numbered keys

## Ideas Welcome

If you have an idea but don't want to implement it, feel free to open an issue to discuss.
