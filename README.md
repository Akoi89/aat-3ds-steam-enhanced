# Ace Attorney Trilogy 3DS: Steam Enhanced

**Capcom's redrawn character art, repainted courtrooms and cleaner evidence icons from the
Steam release of the Ace Attorney Trilogy, carried onto the US 3DS game, with most of the
animation frames the 3DS version cut put back.**

The 3DS trilogy (*Phoenix Wright: Ace Attorney*, *Justice for All* and *Trials and
Tribulations*) uses the older art. The Steam release redrew the characters and repainted some
of the backgrounds. This patch moves that art into the 3DS game. The 3DS still draws at its
own resolution, so this is not an HD patch: the Steam art is scaled down to fit. The script,
the music and your saves are left alone.

What the patch changes, screen by screen, is in [RELEASE_NOTES.md](RELEASE_NOTES.md). This
README is the instructions.

> **You need your own copy of the game.** The patch contains no game files, only the
> differences. It applies to the **US eShop** version (title ID `0004000000138F00`), dumped
> from your own 3DS. There is no EU build.

---

## Before you start: the source file has to be exactly right

The patch turns a **decrypted `.cci`** of the US game into the patched `.cia`. It's strict
about the source, and a file of the right size isn't necessarily the right file.

> **Dump the game encrypted, then decrypt it on your PC.**
> - With GodMode9, dump the installed game to CIA with **no decrypt and no trim**. Where
>   GodMode9 offers **Build CIA (legit)** and **Build CIA (standard)**, pick **legit**:
>   standard decrypts while it builds.
> - GodMode9's own decrypt or trim gives you a file of exactly the right size with different
>   bytes, and the patch refuses it. Running the PC decryptor on that file afterwards doesn't
>   fix it. A matching size is only a first check; the hash of the patched `.cia` at the end
>   is the real proof.

Then decrypt it on the PC:

1. Check the dumped `.cia` is **385,205,248 bytes**. If it isn't, redo the dump before you
   spend time decrypting.
2. Get [Batch CIA 3DS Decryptor](https://gbatemp.net/download/batch-cia-3ds-decryptor.35098/download?version=35152)
   and extract it to a new folder.
3. Put the dumped `.cia` in that folder and run `Batch CIA 3DS Decryptor.bat`.
4. It writes `<your file name>-decrypted.cci` next to it, **385,191,936 bytes**. That `.cci`
   is the source for the patch. Don't rebuild, trim or re-pack it.

Your `.cci` won't hash the same as mine, and that's fine. The decryptor writes random bytes
into a small area of the file header (44 bytes), and the patch is built to ignore that area.
Everything else in the file has to match.

## Files

| file | size (bytes) | SHA-256 |
|---|---:|---|
| `AAT-steam-enhanced-v1.0.1.xdelta` (the patch) | 17,833,155 | `d95b0daed93530b20ed55c03d2a20c7a120da8ee8a461abe87c70606971f1284` |
| the patched `.cia` you'll make | 386,155,520 | `1998cb358e536b16ed3d3245dc7ffbd5b0d3a3a36d34d196dcad0850282cbdba` |

The `.cia` isn't posted anywhere. You make it from your own copy with the patch, then check
its SHA-256 against the table.

## Apply the patch (Windows)

You need a decrypted `.cci` from the section above and one of these two tools.

**With xdelta UI** (a small window for xdelta):

1. Open xdelta UI and go to the Patch tab.
2. Source file: your decrypted `.cci`. Patch: `AAT-steam-enhanced-v1.0.1.xdelta`.
3. Choose where to save the output, and name it `AAT-steam-enhanced-v1.0.1.cia`.
4. Press Patch. It writes a file of 386,155,520 bytes.

**With the xdelta3 command line**, in Windows PowerShell, in the folder that holds the files:

```powershell
.\xdelta3.exe -d -s "your-game.cci" "AAT-steam-enhanced-v1.0.1.xdelta" "AAT-steam-enhanced-v1.0.1.cia"
```

Put the real name of your `.cci` in place of `your-game.cci`. If the patch is applied
against the wrong source, xdelta3 stops with an error.

## Check the result

In Windows PowerShell:

```powershell
Get-FileHash "AAT-steam-enhanced-v1.0.1.cia" -Algorithm SHA256
```

The hash has to be `1998cb358e536b16ed3d3245dc7ffbd5b0d3a3a36d34d196dcad0850282cbdba`. If it is, the source was right and the file is good. If
it isn't, don't install it. See Troubleshooting.

## Install

Copy the checked `.cia` to your SD card and install it with FBI or another CIA installer on
a 3DS with custom firmware. You don't need to delete the original first: it installs over the
US trilogy under the same title ID, so your saves stay where they are. Mine were still there
after installing it over the original. Back them up first anyway; the patch doesn't touch them.

If you're updating from v1.0, apply this patch to your original decrypted `.cci` again. The
patch is built against the original game, so your v1.0 `.cia` can't be its source.

If you have a LayeredFS mods folder for this game (Luma's `luma/titles/0004000000138F00`),
remove or disable it. Files in that folder are loaded instead of the game's own and would hide
the patch.

**To check it took:** the title screen reads **Steam Enhanced v1.0.1** at the bottom right,
under the end of the TRILOGY bar.

The patched `.cia` also runs on Azahar, which is what I used for most of my testing.

## Troubleshooting

- **"target window checksum mismatch."** The source isn't the file the patch was made from. The
  usual cause is that GodMode9 decrypted or trimmed the dump, or built it with Build CIA
  (standard). Dump again as above, then decrypt on the PC.
- **The output has the right size but the wrong hash.** Don't install it. Check that you
  hashed the new output and that the patch file matches the hash in the table. If both are
  right, the source is the problem: dump again as above.
- **xdelta UI reports an error.** Check that the source and patch are the right files and the
  output folder is writable. A checksum mismatch means the source, as in the first item.
- **The title screen doesn't say Steam Enhanced v1.0.1.** Check that the install finished and
  that you started the US trilogy, and remove or disable any LayeredFS mods folder for this
  game, since its files override the patched ones.
- **The decryptor gave me a different file name or no `.cci`.** The patch needs the `.cci` of
  the US eShop game, title ID `0004000000138F00`, dumped from your system as a CIA.

## What has been tested

Finished:

- I tested all three games on the Azahar emulator across many test builds.
- I tested v0.13 on a real New 3DS XL. All three games boot, and I played the start of each
  game's first trial. v1.0 is v0.13 plus the title-screen lettering, nothing else, and I booted
  it on the same console to see the new title screen.
- v1.0.1 is v1.0 with a data-only change, like v1.0: some animation poses now play in the
  right spot, about fifteen animations run at the original 3DS timing, and the title screen
  says v1.0.1. The executable and every picture other than the title logo are the same as v1.0.
  I checked the characters whose poses it moves on the Azahar emulator, by capture. Two of those poses never came up on screen, so I checked them in the data only.
- Late-game scenes and the pieces I fixed late are checked in the data. Several I also checked
  on the emulator by swapping them into early scenes of each game.
- Existing saves load. Mine carried over when I installed the patched game over the original
  on the console, and on the emulator the save files were byte-identical before and after each run.

Not finished:

- I haven't run v1.0.1 on a real 3DS yet.
- Late-game scenes haven't been played on real hardware.
- Some character files are larger than the originals. Every character I brought on screen in the emulator or
  on the console loaded and played correctly. Characters I didn't bring on screen haven't been
  checked that way.

If anything looks wrong, please [open an issue](https://github.com/Akoi89/aat-3ds-steam-enhanced/issues) on this repository. The game, the case and
roughly where you were is enough, and a photo of the screen helps more than a description.

## Known problems

- **A few animations keep some of the original 3DS art.** Steam's picture has a gap in the
  spot, or nothing that lines up, so the original pixels are used there. This is four
  animations in three character files.
- **The ID card and newspaper icons are as unreadable as the original 3DS ones.** I tried
  to improve them, and nothing I made was any clearer, so they stay as they were.
- **One character's cup has a faint one-pixel line in its outline.** Filling the line would erase the
  outline itself.

## Credits

- **Capcom**: the game, and the Steam trilogy art this patch is built from.
- **xdelta3** (Joshua MacDonald) builds and applies the patch.
- **makerom** and **3dstool** build the installable `.cia`.
- **LaMa**, an image inpainting model, extends a few backgrounds where Steam's picture
  doesn't cover the whole 3DS screen.
- **etcpak** helps pack the finished pictures into the 3DS texture format.
- **Azahar** for emulator testing.

The patch was made with Claude (Anthropic) doing the reading, measuring and scripting. Every change was checked against the shipped
files, and on screen wherever I could reach it.

*Phoenix Wright: Ace Attorney Trilogy* is © Capcom. This is an unofficial fan patch and isn't
affiliated with or endorsed by Capcom.

## Thanks

Thanks to GrouchoGlasses42 for their earlier Ace Attorney Trilogy 3DS Missing Frame Restoration Mod. Comparing my results with it helped me work out how to line Steam's art up on the 3DS. This patch was built separately and uses no files or code from it.
