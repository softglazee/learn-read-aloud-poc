# Read-aloud for lesson content: proof of concept

A demonstration for [Learn WordPress issue #3649](https://github.com/WordPress/Learn/issues/3649):
should Learn lessons offer a "listen to this lesson" option, and how should it sound?

**Live demo:** see the GitHub Pages URL for this repository.

It shows one lesson page (*Intro to Block Patterns*) with a free, browser-native "Listen"
button working on the real lesson text, then a comparison of the same passage three ways
(browser voice, a commercial voice, and the lesson's own narrator), plus an Urdu sample using
the reviewed community translation from [Learn #3613](https://github.com/WordPress/Learn/issues/3613).

Demonstration only. Not a proposal to install any service on WordPress.org, and not affiliated
with or endorsed by the WordPress project. Built by Azhar Ali ([@softglaze](https://profiles.wordpress.org/softglaze/)).
Vanilla HTML, CSS and JavaScript, no build step, no dependencies.

## Update, 10 September 2026

Rebuilt the player from the review feedback on the issue. **Every section on the page shares the
same controls**: both lesson players, the two browser-voice comparison rows, the language tester, and
the two commercial voice rows.

- **Speed presets** (0.5x, 1x, 1.5x, 2x) replace the speed slider.
- **Volume is a button.** It opens a small control with volume down, a slider, volume up, a live
  percentage and mute, so the main row stays simple but the level is still adjustable.
- **A position slider** that seeks to the word. `speechSynthesis` has no seek, no `duration` and no
  `currentTime`, so this is built: the lesson is split into sentences, each is measured, and a seek
  starts the utterance partway into a sentence at a word boundary rather than at the top of it.
  Progress is tracked with the API's word `boundary` events, so the bar follows real speech rather
  than a stopwatch. Nudging forward a few seconds now moves a few seconds.
- **Voice selection in a hamburger menu** at the top left of each player, showing the best four
  voices on the viewer's own device. The list is ranked, not alphabetical: names containing
  "Natural", "Neural", "Siri", "Premium" or "Enhanced" are promoted, network voices
  (`localService === false`) are promoted, and "Compact", "eSpeak", "Desktop" and the macOS novelty
  voices are demoted. The tester also carries its language picker in the same menu, and the two
  commercial voice rows use the same menu over their fixed list of pre-generated clips instead of a
  dropdown. The reference clip row has no menu because it has no alternatives to choose from.
- **A written answer on reducing robotic delivery** covering formant vs concatenative vs neural
  synthesis, why SSML is unusable on the browser route, what the three available knobs actually do,
  and per-platform voice quality.

Popovers are placed in JavaScript and clamped into the viewport: hamburger menus align to their
button's left edge, volume popovers centre on theirs, because the volume button wraps to a different
position at narrow widths.
