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

Rebuilt the player from the review feedback on the issue:

- **Speed presets** (0.5x, 1x, 1.5x, 2x) replace the speed slider.
- **Volume is a button** that mutes and unmutes. The fine volume slider moved into the settings menu.
- **A position slider** was added so a listener can rewind or skip forward. `speechSynthesis` has no
  seek, no `duration` and no `currentTime`, so the lesson is split into sentences, each is given an
  estimated length, and the slider restarts at the nearest sentence. Progress inside a sentence is
  anchored to the API's word `boundary` events where the browser fires them, so the bar follows the
  real speech rather than a stopwatch. It lands on sentence boundaries, which is the honest limit.
- **Voice selection moved into a hamburger menu** at the top left of each player, showing the best
  four voices on the viewer's own device. The list is ranked, not alphabetical: voices whose names
  contain "Natural", "Neural", "Siri", "Premium" or "Enhanced" are promoted, network voices
  (`localService === false`) are promoted, and "Compact", "eSpeak", "Desktop" and the macOS novelty
  voices are demoted.
- **A written answer on reducing robotic delivery** was added to the page, covering formant vs
  concatenative vs neural synthesis, why SSML is unusable on the browser route, what the three
  available knobs actually do, and per-platform voice quality.

The universal voice tester keeps its full language and voice pickers on purpose: its job is to let a
reviewer try every voice their device has.
