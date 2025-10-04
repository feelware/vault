## Source

### Environment

```yaml
Natural/Nature
    Body of water
        Ocean
        Stream
        Waterfall
        Underwater
        Rain
	Open air
		Fields
		Deserts
		Farm
		# ...
	Storm/Thunder
	Forest
	Cave
	# ...
Social/Artificial
	Everyday
		Urban
			Park
			Traffic
			Street market
			Onboard
			# ...
		Building
			Home
				Kitchen
				Bathroom
				Living room
			Restaurant
			Office
			Classroom
			Hospital
			Library
			# ...
	Event
		Amusement Ride
		Beach
		Carnival
		Festival
		Party
		Protest
		Sports
		# ...
	Industrial
		Factory
		Construction Site
		# ...
```

- Building: Everyday indoor spaces (e.g. home, businesses)
- Urban: Everyday outdoor or very open spaces, mostly city-oriented
- Events: Social events that escape the everyday routine and are typically loud. Most of them are recreational, although not all (like protests)

- Onboard: Inside public transportation

### Entity/Object

```yaml
Natural/Nature
	Biological
		Botanical/Plant
			Stick
			Leaf
				Celery
				Cabbage
			Fruit
				Tomato
			Root
				Leek
				Potato
			Nut/Seed
				Pistachio
		Zoological
			Body
				Beak
				Nail/Claw
				Teeth
				Feather
				Mouth
				Lungs
				Heart
				Intestines
			Animal
				Amphibian
				Fish
				Bear
				Bird
					Corvids
					Songbird
					Shoebill
				Feline
					Cat
				Canine
					Dog
				Insect
				Primate
				Reptile
				Horse
				Rodent
Human
	Man/Male
	Woman/Female
	Baby
	Child
	Elderly
	Multitude
Fabricated/Artificial
	Furniture
		Chair
		Desk/Table
		Sofa
		Bed
		Pillow
		Shelf
	Appliance
		Refrigerator
		Washing Machine
		Microwave
		Oven
		Dishwasher
		Vacuum Cleaner
		Air Conditioner
		Heater
	Item
		Pencil
		Coin
		Keys
		Bottle
		Glass
		Drink can
		Bag
		Shoe
		Clothing
		Phone
		Paper punch
    Machinery
		Hammer
		Saw
		Chisel
		Drill
		Grinder
    Weapon
	    Melee
	    Gun
	    Explosive
    Vehicle
        Landcraft
            Car
            Motorcycle
            Bicycle
            Truck
            Bus
        Watercraft
            Boat
            Ship
            Submarine
        Aircraft
            Airplane
            Helicopter
            Drone
```

By separating Natural and Biological into different tags, I made space for natural non-biological entities/objects **whose sound is more than just the material they're made of**. I just can't think of an example at the moment. Maybe a volcano.

### Material

```yaml
Natural/Nature
    Geological
        Water
        Gas
	        Air
	        Vapor
	        Fire
	    Aggregate
			Snow
	        Mud/Soil/Dirt               # Dampened
	        Sand                        # Dusty
	        Gravel                      # Rock, Grainy
        Rock
            Rubble                  # Rough
            Pebble                  # Textured
	        Coal
        Mineral
	        Ice
            Crystal                 # Sharp
        Metal                       # Sharp
    Biological
        Botanical
            Bark                    # Rough
            Wood                    # Textured
            Paper                   # Textured
            Cardboard               # Textured
            Cork
            Cotton                  # Fuzzy
            Grass                   # Fuzzy
            Foliage                 # Fuzzy
            Puree
        Zoological
            Bone                    # Sharp
            Fur
			Hair
            Meat
            Skin
            Leather                 # Textured
Synthetic/Artificial
    Polymer
        Plastic
        Foam                        # Fuzzy
        Nylon
        Silicone
        Rubber
    Ceramics                        # Sharp, Resonant
        Porcelain
        Stoneware
        Terracotta
        Brick
        Glass                       # Smooth
```

### Instrument

```yaml
Traditional
	String
	    Bowed
	        Violin
	        Viola
	        Cello
	        Double Bass
	    Plucked
	        Guitar
	            Acoustic
	            Electric
	            Bass
	    Ukelele
	    Banjo
	Percussion
	    Drums
	        Kick
	        Snare
	        Tom
	        Cymbal
	            Hi-Hat
	                Closed
	                Open
	            Ride
	        Fill
	        Break
	Wind
	    Woodwind
	        Flute
	        Clarinet
	        Zampoña
	    Brass
	        Trumpet
	        Trombone
	        Tuba
	Keyboard
	    Piano
	        Upright Piano
	        Felt Piano
	    Organ
Synth
	Drum Machine
	    Clap
	Bass
	    Reese
	    Neuro
	    Square 4
	    Growl
	    Sub
```

## Properties

### Mixing properties

```yaml
# Highs
Harsh
Bright
Dark
# Lows
Bassy
Muddy
Thin
# Loudness
Soft
Loud
Compressed
# Inharmonicity
Inharmonic
Harmonic
# Depth
ASMR
Close
Distant
# Width
Mono
Wide
Panned
```

### Timbral properties

```yaml
Solid/Rigid
	Brittle/Sharp
	Resonant
	Smooth
	Textured
	Rough
	Ductile
	Damped
Liquid
	Watery
	Carbonated
	Creamy/Gory
	Oily
	Steamy
Amorphous
	Gaseous
	Grainy
	Dusty
	Fuzzy
```

- Oily: Low viscosity
- Creamy: High viscosity

## Action

```yaml
Strike
    Hit
    Clap
    Snap
    Drop
    Crash       # Break
    Shoot
    Explode     # Combust
    Walk
    Stomp
Break
    Crush
    Cut
    Split
    Bite
    Tear/Rip
Friction
    Rub
    Roll
    Slide
    Scratch
    Squeak
Deform
    Press
    Squeeze
    Bend
    Squash
    Crumple
Move
    Swing
    Shake
    Rattle
    Jingle
Fluid dynamics  # Liquid
    Splash      # Strike
    Drip
    Flow
    Bubble
    Gurgle
    Sizzle
Aerodynamics
    Flap        # Move
    Whoosh
    Whistle     # Vocalize
    Hiss
    Blow
    Puff
    Sigh        # Vocalize
    Fart
    Spray       # Fluid dynamics
Combust
    Burn
    Ignite
    Smolder
Vibrate
    Hum
    Buzz
    Ring
Vocalize
    Speak
    Shout
    Sing
    Rap
    Yawn
    Whisper
    Moan
    Babble
    Cry
    Laugh
    Sneeze
    Growl
    Chirp
    Bark
    Howl
```

## Music Info

### Function

```yaml
Percussive
	Base
	Top
	Perif
	Cym
Tonal
	Key
	Pluck
	Swell
	Stab
	Pad
Riser
Downer
Texture
Ear candy
One-shot
Loop
	Pulse
	Vocal Chop
	Break
	Fill
```

These tags roughly describe how volume changes over time, but most importantly, they define a sound's function in a song. You might recognize some of these names from preset categories in synthesizers, but some of them are more esoteric.

- Base: A kick-like sound, or anything that can be used as a (conventional or super weird) kick, even some foley can be categorized as Base
- Top: A snare/clap like sound
- Perif: Stands for "peripheral": tom-like sounds that can be used as secondary percussion. Again, a lot of foley and glitches go here
- Cym: Noisy, cymbal-like sounds: fast attack a relatively short decay
- Pad: Sustained, evolving sound with long attacks and decays
- Pulsation: Tremolo-like
- Pluck/Key: Fast attack and medium decay, but for pitched sounds
- Texture: No distinctive elements, can be easily used as a layer for other sounds
- Ear candy: Foley/designed sounds to use as filler

### Tonality

```yaml
Polyphony
	Monophonic
	Polyphonic
		Major chord
		Minor chord
		Augmented
		Diminished
		Extended
Scale
    Major scale
    Minor scale
Root
    C
    C#/Db
    D
#   ...
    B
```

These tags are very useful for finding material to feed granular synths with. If I want anything pitched, the "Tonality" tag is often enough, or a specific scale and root if I'm doing it in the context of a song. In fact, scale tags should be used *only* for melodies and chord progressions. It wouldn't make sense to tag a sample containing a single chord with a specific scale, since that chord can be used in multiple scales.

- Root tags can be used to define:
	- the root of the scale of a **melody, chord progression, or full song**
	- the note of a **single-note sample**
	- the root of the chord of a **single-chord sample**
- If using both Scale, Chord, and Root tags simultaneously (e.g. to tag a song in D minor with the chords Dm, Bb, and C), the root tag should be interpreted as the root of the *scale*, **not the root of any of the chords**, so in this case the root tag would be "D", not Bb nor C. In total, only these tags must be used:
	- D (Root)
	- Minor scale
	- Major chord
	- Minor chord
- This also applies for melodies. For example, a melody in D minor with notes D, F, and A must have *only* the following tags:
	- D (Root)
	- Minor scale

In the future, I envision encoding more specific music information (such as all notes and chords played in the file) as some sort of metadata.

I might add tags for microtonal music in the future.

### Player count

```yaml
Solo
Duet
Quartet
Ensemble/Band
```

### Playing technique

```yaml
Bowing
Pizzicato
Plucking
Slapping
Striking
Strumming
Humming
Tremolo
```

## Genre/Style Info

```yaml
Classical
Electronic
	Dubstep
		Riddim
		Brostep
	Breakbeat
	Jungle
	Hyperglitch
#   ...
International
	Latin
		Merengue
		Afro-Cuban
		Salsa
		Samba
#       ...
#   ...
```

## Semantic Info

```yaml
Intent
    Narration
    Lecture
    Question
    Insult
    Presentation
    Speech
#   ...
Topic
    Politics
    Love
    Weather
    History
    Religion
#   ...
Sentiment
    Angry
    Remorseful
    Romantic
    Ironic
#   ...
```

I use these tags to further describe speech and lyrics in terms of the actual ideas being transmitted. Sentiment tags can also be used to describe certain non-speech sounds based on your own perception.

## Processing Info

```yaml
Unprocessed
Subtractive/Analog
Physical Modelling
Granular
    Concatenative
Spectral
    Spectral Gate
    Spectral Resynthesis
#   ...
Modulation
    Flanger
    Phaser
    Chorus
Sine Compression
FM/AM
Stutter
# ...
```

## Gear Info

```yaml
Hardware
    Eurorack
    Guitar Pedal
    Analog
Digital
    Software
        Cardinal
        Vitalium
        Surge XT
        SoundThread
        Cecilia
#       ...
```

Gear used to make the sound.

## Geographical Info

```yaml
Asia
Americas
    Northern America
        USA
        Canada
    Latin America
        Mexico
        Central America
        Caribbean
        South America
            Peru
                Lima
#               ...
#           ...
Europe
Africa
Oceania
```

## Language

```yaml
English
    American
    British
#   ...
Spanish
    Peruvian
	    Limeño
#       ...
    Spaniard
#   ...
Portuguese
    Brazillian
    Portugal
# ...
```

## Meta

```yaml
File
	Wavetable
	IR
	Render
		Stem
		Track
	Preset/Patch
Authorship
	Original
	Derived
	Downloaded
License
	Creative Commons
	    CC0
	    CC-BY
	Copyrighted
```

Some clarifications:

- Render: Any piece of music that comes out of a DAW, finished or not
- Stem: Rendered group of instruments
- Track: Full song
