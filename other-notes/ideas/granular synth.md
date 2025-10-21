# Granular resynthesis of tonal audio using polyphonic pitch detection

## Core idea

- Splice an audio file into tiny fragments
- Use polyphonic pitch detection to assign each fragment to either an **individual pitch** (if the fragment is monophonic) or a **chord quality** (if it's polyphonic)
- If a *single* MIDI note is received, play back fragment associated to that note (candidates)
- If a note with no associated fragments is played, select fragments with the closest pitch and pitch them up/down to fit
- If a chord is played (eg. CMaj7), either find a fragment whose chord shares the same quality (eg. DMaj7) and pitch it up/down to fit (in this case, pitch down), or reconstruct it using a combination of individual notes and/or chords with simpler voicings (option 1: C + E + G + B; option 2: CMaj + B), pitching up/down if necessary
- Offer multiple candidate selection strategies that either maximize continuity (prefer pitch correction over sample position skipping), minimize pitch correction, etc

## Possible expansion: Timbre-based candidate selection

Note that this expansion may double the amount of effort and expertise required, so I might leave it for another time

- Fragments will be plotted as dots in a 2D map according to their timbre: if two fragments are "the same instrument", then they will be closer to each other, even if their pitch is not the same (think of XO or AudioStellar)
- Naturally, clusters would emerge. They would represent specific instruments in the song (vocals, winds, strings, even atonal elements)
- Only the dots corresponding to the current MIDI input (candidates) will be "lit", the rest will be dimmed, meaning that they won't be played
- By default, the entire map is considered for playback, but you can constrain it to a smaller subsection (e.g. just the vocals) represented as a circle whose radio and centroid you can modulate/automate
