# Open with Antigravity IDE — Windows context-menu entry

Adds an **"Open with Antigravity IDE"** option to the Windows right-click menu for
files, folders, and folder backgrounds — so you can open anything directly in
[Google Antigravity IDE](https://antigravity.google/).

After Google split the standalone **Antigravity** app from **Antigravity IDE**, the
old registry tweaks broke: they pointed at `Antigravity.exe`, which no longer exists.
The IDE's executable is now named **`Antigravity IDE.exe`**. These files target the
correct executable.

## Files

| File | What it does |
|------|--------------|
| `install-open-with-antigravity-ide.reg` | Adds the "Open with Antigravity IDE" right-click entry. |
| `uninstall-open-with-antigravity-ide.reg` | Removes the entry. |

All keys live under `HKEY_CURRENT_USER`, so no administrator rights are needed and no
reboot is required.

## Install

1. Double-click `install-open-with-antigravity-ide.reg` and confirm the prompt.
2. Right-click any file or folder — **Open with Antigravity IDE** now appears.

No editing needed. The paths use the `%LOCALAPPDATA%` variable, which Windows expands
to each user's own `C:\Users\<you>\AppData\Local` folder — so the same file works on
any account without changes. (This is why the values are stored as `REG_EXPAND_SZ`,
written in the `.reg` as `hex(2):` lines — a plain string would not expand the
variable.)

> **System-wide installs:** if you installed Antigravity IDE to
> `C:\Program Files\Google\Antigravity\` instead of the default per-user location,
> `%LOCALAPPDATA%` won't match. In that case edit the paths to point there, or use a
> script-based installer that auto-detects the executable.

## Uninstall

Double-click `uninstall-open-with-antigravity-ide.reg` and confirm. The right-click
entry is removed immediately.

> **Note:** the uninstall file contains no executable path — it only *deletes* the
> registry keys the installer created (the `-` prefix on each key means "delete this
> key"). It works as long as its key name matches the installer's, which it does
> (`Antigravity`).

## How it works

The installer writes a shell verb named `Antigravity` to three locations so the
entry shows up everywhere:

- `Software\Classes\*\shell\Antigravity` — on individual files (`%1` = the file)
- `Software\Classes\Directory\shell\Antigravity` — on folders (`%V` = the folder)
- `Software\Classes\Directory\Background\shell\Antigravity` — on empty space inside a
  folder (`%V` = the current folder)

Each verb's `command` subkey launches `Antigravity IDE.exe` with the selected path,
and the `Icon` value gives the menu item the app's icon.

## License

Public domain / do whatever you want.
