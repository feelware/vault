# Ideas for Cardinal modules

- modules for interacting with TagStudio library and feed modules with
	- consider allowing to feed more than one module
- modules for interacting with Ardour session: getting the output of any channel, creating automation, bouncing, etc
- modules for interacting with AudioStellar
	- one parent module. multiple child modules per AudioStellar unit

## Library Suite

Modules:
- [Library](#Library)
- [Query Concat](#Query%20Concat)
- [Library Preview](#Library%20Preview)
- [Multisampler](#Multisampler) (yet to be designed)
- SamplerX (yet to be designed)
	- "Holy grail of sample reusability"
	- Receives multiple samples and assigns segments of these to particular notes or chords, so that they can be played according to certain rules:
		- to play chords, existing chords (of the same quality but possibly different root note) are pitched up, down, or complemented with other notes
		- to play single missing notes, closest existing notes are pitched up or down to match
		- original notes and chords are preferred by default, this behavior can be "inverted" to maximize stretching/pitch shifting artifacts
		- several time stretching/pitch shifting algorithms should be provided (ideas: granular, spectral, rubber band, paulstretch, etc). their settings should be modulatable
		- options to detect meaningful segments of a sound should be provided (transient detection, silence padding, etc) as well as options to stretch them to fit certain time intervals
		- amount of original pitch/continuity/duration preservation should be modulatable
- Selections Library (yet to be designed)
	- Like Library but for VCV selections, including patching points to make hot-swapping easy (consider creating a template system for this, or following Stoermelder's STRIP BAY model).

### Library

![](../../utilities/attachments/Pasted%20image%2020250814180326.png)

"Current sample" = Currently playing or most recently played sample

- Sample list is scrollable
- Queries are executed on debounced input change
- `CAT` input receives the output of a [*Query Concat*](#Query%20Concat) module, concatenating the input query to its own
- `ADD` button adds the current sample to a new slot of the [*Multisampler*](#Multisampler) next to *Library*
- `REPL` doesn't add to a new slot, but replaces the content of the current slot
- If either `ADD` or `REPL` are pressed and no instance of [*Multisampler*](#Multisampler) is next to *Library*, a new instance is created
- `NEXT` button immediately plays the sample next to the current one
	- `PREV` behaves the same way
- `PLAY` re-plays the most recently played sample, or pauses the currently playing sample
- `LOOP` switch toggles sample looping
- Available `SORT` options (either ascending or descending)
	- Random
	- Filename
	- Filepath
	- Duration
- "Add entire page" menu options adds every sample on the current page to new slots of the [*Multisampler*](#Multisampler) next to *Library*
- Below the sample filename, there's a list of all the tags given to the sample
	- Clicking on a tag adds it to the current query (doesn't clear it)
	- The list should be limited to a single line by default, with a "show more" option that extends the view vertically so that all tags are shown
- Clicking on the waveform of a sample should immediately play it at that timestamp
- The play/pause buttons should behave the same way as the `PLAY` button, changing its icon to "pause" when playing, and to "replay" when done playing
	- Holding Ctrl should change all these buttons' icons to "plus", behaving like `ADD` when clicking them
	- Holding Ctrl+Alt should change all the icons to "replace", behaving like `REPL` when clicking them
- At the end of sample list there should be buttons to change page. It may seem redundant, since there already are buttons to change page, but it minimizes mouse movement with no screen real-estate penalty

### Query Concat

![](../../utilities/attachments/Pasted%20image%2020250814175917.png)

- Not only it can output a query, but it can also receive input from another *Query Concat* instance, concatenating the input query to its own. This allows to create a "hierarchy" of queries
- *Query Concat* shows a list of all queries it is concatenated to
- "Global query" menu options implicitly concatenates the current query to all [*Library*](#Library) instances.

### Library Preview

![](../../utilities/attachments/Pasted%20image%2020250814175837.png)

- This module receives the preview output of all *Library* modules
- A single instance per patch 
- You may want to connect it to an aux audio output (like your headphones), or to the main output if you want. You can even connect it to an effect chain (e.g. for limiting)

### Multisampler
