# Life — v0.9 private alpha

Thanks for testing. This is an early alpha — expect rough edges (see Known
issues below). Ad-hoc signed, not notarised, so there's a one-time Gatekeeper
step on first launch.

Copyright © 2026 Joel Eaton. All rights reserved. This build is provided solely for private testing. It may not be copied, redistributed, published, decompiled, or shared with anyone outside this test. No licence or rights are granted beyond running it to evaluate it. Please don't circulate the files or the download link.

Life 0.9 is unfinished software: there are no factory presets, some features are incomplete or unverified (see Known issues), and it may crash or behave unexpectedly. Please don't use it on anything you can't afford to lose, and save your work often.

## Install

The build is ad-hoc signed, not notarised, and the files pick up macOS's download quarantine on the way to you — so macOS will block them on first open until you clear it. This is expected.

Unzip and copy the components to:
AU → ~/Library/Audio/Plug-Ins/Components/Life.component
VST3 → ~/Library/Audio/Plug-Ins/VST3/Life.vst3
Standalone → wherever you like (e.g. /Applications)
Clear the download quarantine. Open Terminal and run, adjusting paths if needed:
   xattr -dr com.apple.quarantine ~/Library/Audio/Plug-Ins/Components/Life.component
   xattr -dr com.apple.quarantine ~/Library/Audio/Plug-Ins/VST3/Life.vst3
   xattr -dr com.apple.quarantine /Applications/Life.app
First launch of the standalone: if macOS still warns of an unidentified developer, open System Settings → Privacy & Security and click Open Anyway in the note near the bottom. You only do this once.
In your DAW, rescan the plug-in list if Life doesn't appear.

# Reporting bugs

Please quote the version (0.9) in any report, and note whether you were in the plug-in or standalone, and which host. If a patch is involved, save it embedded before sending so it opens on my machine without your audio files.

## First-launch Gatekeeper step (once per format)

macOS will warn that the plug-in is from an unidentified developer the first
time you open it. Open **System Settings → Privacy & Security** and click
**Open Anyway** in the note near the bottom. Do this once per plug-in. In
your host: re-scan the plug-in library if it's not appearing.

## Reporting bugs

Please reference **v0.9** in any report. If you're sending a patch/preset
that uses sample-embedding, save it with embed **on** first — a
non-embedded patch points at your local file paths and won't load on
another machine.

## Known issues

- No factory presets yet — only user presets (`.lifeinstr` files).
- Novation Launch Control XL 3 template is partial: extra mapping modes are
  deferred pending a MIDI-learn design pass.
- LED feedback to the XL 3 sits behind a flag and may not be fully verified
  in every mode.
- MIDI has only been verified in the Standalone app — hosted-plugin (AU/VST3)
  MIDI behavior in a DAW is unverified.
- Per-source live input selection (multichannel) is **standalone-only**. In
  a DAW, live-input sources read the shared stereo sidechain instead of a
  per-source channel pick.
- Aux direct-outs are tapped pre-master, so stems will sound noticeably
  drier than the main mix — this is intentional, not a bug. **In the AU
  format specifically**, this exclusivity doesn't apply: Logic/Ableton's AU
  wrapper reports every aux bus as enabled from load regardless of whether
  you've actually routed it, so on AU every source always also sums into
  the main mix even when its aux out is wired up elsewhere. VST3 and
  Standalone behave as designed (a routed aux with "Parallel Out" off pulls
  that source out of main).
- Sample storage supports reference, collect-&-embed, and relink-by-hash —
  all shipped and working; just remember the embed note above when sharing
  patches.
- Manual per-step velocity + pitch editing on frozen/hand-edited pattern
  lanes landed late in this cycle (left-click = toggle, vertical drag =
  velocity, right/ctrl-click = quick accent, alt+drag = pitch). It's in and
  working, but has had less soak time than the rest of the release — flag
  anything that feels off.

Version: 0.9
