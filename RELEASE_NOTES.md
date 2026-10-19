# Release Notes

This patch brings the character art, the repainted backgrounds and the evidence icons from Capcom's Steam release of the Ace Attorney Trilogy onto the US 3DS version, and puts back many of the animation frames the 3DS release cut. It's an xdelta patch you apply to your own copy of the game, with an optional LayeredFS zip for Luma3DS, and it leaves the dialogue, the music and your saves alone.

## What this build does

- **Characters use the Steam art.** Every character's sprites are replaced with Capcom's redrawn versions from the PC trilogy, in all three games. They're scaled down to the 3DS's own resolution, because the 3DS screen still draws at its own size, so this isn't HD. What you get is cleaner outlines and the shading and colours of the redraw instead of the older art.
- **Cut animation frames are back.** The 3DS release dropped a lot of the in-between frames that the PC version has: the half-closed eye in the middle of a blink, the in-between steps of a gesture. Most of them are restored, so people move less stiffly. Sounds that play during an animation still land on the same moments as before.
- **The repainted backgrounds.** Steam repainted only some of its backgrounds, and I ported those: the courtroom views, the court lobby, the judge's bench, the sepia-toned courtroom shots and a few others. Where Steam tints a picture while the game runs, I recreated the 3DS version's tint on Steam's painting, so those scenes keep their mood. Every background Steam didn't repaint stays exactly as it was.
- **Evidence icons.** The Court Record pictures and their small thumbnails use Steam's art wherever it looks clearly different from the 3DS copy. They're cleaner, and the colours are graded differently. In the first game, for example, the attorney's badge is gold instead of bronze. Icons that already matched were left alone.
- **A few small picture fixes.** The 3DS stores some Court Record captions as pictures, and a handful were misspelled. I fixed those using the game's own letters, so they look like they were always there. The lettering on some book-cover icons was redone from the 3DS cover's own pixels.
- **The title screen shows the build.** "Steam Enhanced v1.0.1" now appears at the bottom right, in the same style as the rest of the logo, so you and anyone you're helping can see which version is installed.
- **Gameplay and saves.** The dialogue, music and menus are unchanged, and your existing saves carry on working.

## Version history

- **v1.0.1**: in the animation sets of a few characters, some poses were assigned to the wrong spot, so a scene could show the wrong version of a character, such as a different outfit or expression than the original game plays there. Each spot now plays the animation the original 3DS game assigns it. About fifteen animations also played noticeably faster or slower than on the original 3DS, because restored frames had changed their length, and their timing now follows the original. The title screen reads "Steam Enhanced v1.0.1". The executable and every picture other than the title logo are the same as v1.0. There is also a LayeredFS zip for Luma3DS now, so you can copy two files to your SD card instead of building a `.cia`.
- **v1.0**: the first public release. Earlier builds were private test builds.

## What has been tested

Finished:

- I tested all three games on the Azahar emulator across many test builds and looked at the screens myself.
- I tested an earlier build, v0.13, on a real New 3DS XL. All three games boot, and I played the start of each game's first trial with nothing wrong. v1.0 was that build plus the title-screen lettering, and I booted it on the same console to see the new title screen.
- v1.0.1 changes data only, as v1.0 did. I checked the characters whose poses it moves on the Azahar emulator, by capture. Two of those poses never came up on screen, so I checked them in the data only.
- The scenes that come late in each game are checked in the data. For the pieces I fixed late in development, I also swapped them into early scenes on the emulator so I could see them drawn.
- Existing saves work. The save files were byte-identical before and after each emulator run.
- The LayeredFS zip: I booted the original game on Azahar with only its two files loaded, and the title screen showed v1.0.1.

Not finished:

- I haven't run v1.0.1 on a real 3DS yet, by either route.
- I haven't played the late-game scenes on real hardware.
- Some of the character files are larger than the ones they replace. Every character I brought on screen in the emulator or on the console loaded and played correctly. Characters I didn't bring on screen haven't been checked that way.

If something looks wrong, please [open an issue](https://github.com/Akoi89/aat-3ds-steam-enhanced/issues) on this repository. Tell me which game and case you were in, and roughly where. A photo of the screen helps more than a description does.

## Known problems

- **A few animations keep some of the original 3DS art.** In those spots Steam's picture has a gap, or nothing that lines up with the 3DS version, so I used the original pixels. It affects a small number of animations, and the rest of the characters are unaffected.
- **The ID card and newspaper icons are as hard to read as the 3DS ones.** I tried to improve them and nothing I made was any clearer, so they stay as they were.
- **One character's cup has a faint one-pixel line in its outline.** Closing the line would erase the outline itself, so I left it.

## Files

- The xdelta patch for the US game. It contains no game files, and you need your own copy of the game.
- The LayeredFS zip for Luma3DS, optional. It holds the game's changed graphics archive (about 115 MB), so unlike the xdelta it is a modified copy of one of the game's files, and it only works with the original US game installed.
- The README, with the exact steps, file sizes and SHA-256 hashes.

With the xdelta you make the installable `.cia` yourself by applying the patch to a decrypted dump of your own US game. The [README](README.md) has the dump method, the patching steps and the hash check. The LayeredFS route has its own short steps in the same README.

## Credits

- **Capcom**: the game, and the Steam trilogy art this patch is built from.
- The tools I used are credited in the [README](README.md).

Thanks to GrouchoGlasses42 for their earlier Ace Attorney Trilogy 3DS Missing Frame Restoration Mod. Comparing my results with it helped me work out how to line Steam's art up on the 3DS. This patch was built separately and uses no files or code from it.

The patch was made with Claude (Anthropic) doing the reading, measuring and scripting. Every change was checked against the shipped files, and on screen wherever I could reach it.
