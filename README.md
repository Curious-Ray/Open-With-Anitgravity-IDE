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

1. **Edit the path first.** Open `install-open-with-antigravity-ide.reg` in a text
   editor and replace `omnig` in every path with your own Windows username, so it
   points to your install:

   ```
   C:\Users\<YourUsername>\AppData\Local\Programs\Antigravity\Antigravity IDE.exe
   ```

   > Tip: confirm the exact path by finding `Antigravity IDE.exe` on your machine. If
   > you installed system-wide it may instead be under
   > `C:\Program Files\Google\Antigravity\`.

2. Double-click the `.reg` file and confirm the prompt.
3. Right-click any file or folder — **Open with Antigravity IDE** now appears.

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
