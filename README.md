# Quode Palette Storage

A fast disk space analyzer for Windows. It shows what is taking up room on your drives as a colored treemap, so the big files and folders are easy to spot and clean up.

[**Download the latest version**](../../releases/latest)

<p align="center">
  <img src="docs/Screenshot1.png" alt="Quode Palette Screenshot" width="100%">
  <b>Screenshot I</b>
</p>

<table>
    <td width="50%" align="center">
      <a href="docs/audio.png"><img src="docs/Screenshot2.png" alt="Screenshot" width="100%"></a>
      <br>
      <b>Screenshot II</b>
      <br>
      <!-- <sub>Convert common audio formats with FFmpeg</sub> -->
    </td>
    <td width="50%" align="center">
      <a href="docs/video.png"><img src="docs/Screenshot3.png" alt="Screenshot" width="100%"></a>
      <br>
      <b>Screenshot III</b>
      <br>
      <!-- <sub>Convert common video formats with FFmpeg</sub> -->
    </td>
</table>
<table>
    <td width="50%" align="center">
      <a href="docs/audio.png"><img src="docs/Screenshot4.png" alt="Screenshot" width="100%"></a>
      <br>
      <b>Screenshot IV</b>
      <br>
      <!-- <sub>Convert common audio formats with FFmpeg</sub> -->
    </td>
    <td width="50%" align="center">
      <a href="docs/Screenshot5.png"><img src="docs/Screenshot5.png" alt="Screenshot" width="100%"></a>
      <br>
      <b>Screenshot V</b>
      <br>
      <!-- <sub>Convert common video formats with FFmpeg</sub> -->
    </td>
</table>

## Why use it

- **Fast.** Scans a whole NTFS drive in a few seconds by reading the drive's file table directly.
- **Easy to read.** Every drive, folder and file is a block, sized by how much space it uses. Click a block to select it, double click a folder to open it.
- **Safe cleanup.** Right click anything to move it to the Recycle Bin. Windows itself is protected: system folders and files cannot be deleted from the app, and risky items need two confirmations.
- **Private.** The app never connects to the internet. Nothing is collected or sent anywhere.
- **Light and dark themes.** Follows Windows, or switch with one click.

## Download and install

Open the [latest release](../../releases/latest) and pick one of the files under **Assets**:

| File | What it is |
| --- | --- |
| Setup `.exe` | The installer. Recommended for most people. Installs for your user account and adds a Start Menu shortcut. |
| Portable `.exe` | Just the app, no installation. Put it anywhere and run it. |

**Requirements:** Windows 10 or 11, 64-bit. The app uses the WebView2 runtime that is already part of Windows 11 and current Windows 10. The installers download it for you if it is missing.

## First run

Quode Palette Storage asks for administrator rights every time it starts (the Windows UAC prompt). That is how it reads the drive's file table for the fast scan. It only reads; it changes nothing on your drives unless you ask it to move an item to the Recycle Bin or empty the Recycle Bin.

## Using it

1. The drives on the left show how much space is left on each one, with a usage bar. Pick a drive to scan it, or choose a folder to scan just that folder.
2. Look at the treemap. Big blocks are big files or folders. Colors show the type: video, images, audio, documents, archives, apps and other. Folders use deep tones.
3. Click a block to see its details. Double click a folder to go into it, and use the path at the top, the up button or Backspace to go back.
4. Hover over very small blocks to get a magnifier card that makes them easy to click.
5. Right click a block or an item in the list for **Open**, **Show in Explorer**, **Copy path** and **Move to Recycle Bin**. Right click the Recycle Bin folder to empty it.

On a whole drive you may see a block called **Unaccounted space**. That is space Windows counts as used but the scan cannot read, such as restore points and protected system data.

### Minimize to the system tray

The switch in the footer is off by default. Turn it on and minimizing the window hides it to the system tray instead of the taskbar. Click the tray icon, or right click it and choose **Open Quode Palette Storage**, to bring the window back. The tray menu also has **Quit**. Closing the window with the X button quits the app.

### Only one copy runs

If you start the app while it is already open, the open window is brought to the front and a message tells you it is already running.

## Delete safety

Deleting is checked twice, in the interface and again inside the app.

- **Protected, never deleted from the app:** whole drives, Windows, Program Files, ProgramData, Users and every user profile folder, personal folders such as Documents and Desktop (the files inside them are fine), AppData and the folders directly inside it, system recovery and boot folders, the Recycle Bin itself, and system files such as `pagefile.sys` and `hiberfil.sys`.
- **Stronger warning, two confirmations:** anything inside Program Files or ProgramData, data inside AppData, Windows upgrade leftovers (including `Windows.old`), and anything on a removable drive or network location.
- **Everything else:** one confirmation.

Deleting moves the item to the Recycle Bin, so you can restore it. Windows decides whether the item fits, though: if it is larger than the Recycle Bin allows, or the Recycle Bin is turned off for that drive, Windows may delete it permanently. Removable drives and network locations have no Recycle Bin, so deletes there are always permanent. The confirmation dialog tells you which applies.

For Windows leftovers such as old updates and temporary files, Disk Cleanup is still the safest tool.

## Good to know

- Sizes are the space used on disk, so they should closely match what Windows shows. Hard linked files are counted once.
- Drives that are not NTFS, and folders you pick, use a slower standard scan that reports file length, so numbers can differ a little.
- Each folder shows its 200 largest items. Smaller ones are grouped into one block.
- Scanning a drive with millions of files can use a gigabyte or more of memory while it runs.
- Some protected areas cannot always be read. They appear as unaccounted space.

## Troubleshooting

**Windows says it "protected your PC" when I run the installer.** New apps that Windows has not seen often are checked by SmartScreen. Choose **More info**, then **Run anyway**. If you would like to check the file first, see Verify your download below.

**The app says the standard scan was used.** The fast scan needs an NTFS drive and administrator rights. If you chose a folder, or the drive is not NTFS (for example a USB stick formatted as exFAT), the standard scan is used instead and works fine, just slower.

**I clicked the tray icon but cannot see the window.** Check the taskbar and the hidden icons arrow next to the clock, then click the tray icon again.

**The app icon in File Explorer looks old after an update.** Windows caches icons. Run `ie4uinit.exe -show` from a command prompt, or restart Explorer.

## Verify your download

Each release includes a `SHA256SUMS.txt` file. To check a download, open PowerShell in your Downloads folder and run:

```powershell
Get-FileHash .\<file name> -Algorithm SHA256
```

The hash printed should match the line for that file in `SHA256SUMS.txt`.

## Uninstall

- **Installed version:** Settings, then Apps, then Installed apps, then Quode Palette Storage, then Uninstall.
- **Portable version:** close the app and delete the file.

The app's few settings (theme and the tray switch) are stored in `%LOCALAPPDATA%\com.quodepalette.storage`. The uninstaller offers to remove them; for the portable version you can delete that folder.

## Font

The interface uses Montserrat (Medium and SemiBold), which is licensed under the SIL Open Font License. The license text is in `ui/fonts/OFL.txt` so keep it next to the fonts.

## Feedback

Found a bug or have an idea? Open an issue on this repo, or reach us at [hello@quodepalette.com](mailto:hello@quodepalette.com).

## License

Released under the [PolyForm Noncommercial License 1.0.0](LICENSE). You are free to use, modify and share it for personal, educational and other noncommercial purposes. For commercial use, please get in touch.
[Email Us](mailto:hello@quodepalette.com)
