## Source

### Environment

```yaml
Natural
    Terrestrial
        Forest
        Desert
        Mountain
        Tundra
    Aquatic
        Ocean
        Lake/River
        Underwater
    Atmospheric
        Wind
        Storm
Artificial
    Domestic
        Kitchen
        Bathroom
        Living Room
    Social
        Business/Institution
            Restaurant/Bar
            Airport
            Mall
            Supermarket
            Theater
            Library
            Museum
            Hospital
            School
            Office
            Factory
            Prison
        Urban
            Park
            Playground
            Traffic
            Street Market
            Public Transport
            City
            Subway
            Construction Site
            Beach # Ocean
```

### Entity/Object

```yaml
Natural
    Biological
        Plant
            Tree
            Flower
            Grass
            Leaf
            Fruit
            Vegetable
            Mushroom    # (technically fungi)
            Root
        Animal
			Organ/System
				Mouth
				Lungs
				Intestines
			Organism
	            Human
	                Male
	                Female
	                Baby
	                Adult
	                Child
	                Elderly
	                Multitude
	            Non-human
	                Amphibian
	                Aquatic
	                Bat
	                Bear
	                Bird
	                    Bird of Prey
	                    Songbird
	                    Sea Bird
	                    Tropical Bird
	                Feline
	                    Cat
	                    Lion
	                Canine
	                    Dog
	                    Wolf
	                Insect
	                Primate
	                Reptile
	                Rodent
Artificial
    Furniture
        Chair
        Table
        Sofa
        Bed
        Cabinet
        Shelf
        Desk
    Appliance
        Refrigerator
        Washing Machine
        Microwave
        Oven
        Dishwasher
        Vacuum Cleaner
        Air Conditioner
        Heater
    Tool
        Hand Tool
            Hammer
            Screwdriver
            Saw
            Chisel
        Power Tool
            Drill
            Grinder
            Sander
    Weapon
        Melee
        Firearm
        Siege
    Explosive
        Grenade
        Bomb
        Mine
    Vehicle
        Land
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

### Material

```yaml
Natural
    Geological
        Water
        Air
        Vapor
        Soil/Mud                    # Dampened
        Sand                        # Dusty
        Rock
            Rubble                  # Rough
            Pebble                  # Textured
            Gravel                  # Grainy
        Mineral
            Crystal                 # Sharp
            Coal
        Metal                       # Sharp
            Hard                    # Smooth
            Foil                    # Textured
    Biological
        Botanic
            Bark                    # Rough
            Wood                    # Textured
            Paper                   # Textured
            Cardboard               # Textured
            Cork
            Cotton                  # Fuzzy
        Zoological
            Osteous                 # Sharp
                Bone
                Horn
                Nail
                Shell
                Tooth
                Claw
            Furry                   # Fuzzy, Damped
                Wool
                Fur
                Hair
                Feather
            Insides
                Meat
                Viscera
                Blood
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
String
    Bowed
        Violin
        Viola
        Cello
        Double Bass
    Plucked
        Guitar
            Acoustic Guitar
            Electric Guitar
            Bass Guitar
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
```

### Designed

```yaml
Drum Machine
    Clap
Synth Strings
Designed Bass
    Vintage
    Reese
    Neuro
    Square 4
    Growl
    Sub
```

This category will probably evolve over time.

## Properties

```yaml
Timbral
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
	Distant/Verb
    # Position
	Center
	Sides
    # Width
	Mono
	Stereo
Textural
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
        Creamy
        Oily
 		Pasteous
        Steamy
    Amorphous
        Gaseous
        Grainy
        Dusty
        Fuzzy
```

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
    Chirp
    Bark
    Cry
    Laugh
    Moan
    Growl
    Shout
    Babble
    Speak
    Sing
    Rap
    Whisper
    Yawn
```

## Musical Info

```yaml
Player Count
    Solo
    Duet
    Quartet
    Ensemble/Band
Polyphony
    Monophonic
    Polyphonic
        Chord
            Major
            Minor
            Augmented
            Diminished
            Triad
            Extended
Playing Technique
    Bowing
    Pizzicato
    Plucking
    Slapping
    Striking
    Strumming
    Humming
    Tremolo
Function/Envelope
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
    Earcandy
    One-Shot
    Loop
	    Pulse
	    Vocal Chop
	    Break
		Fill
Octave
    0
    1
    2
#   ...
    7
Scale
    Major
    Minor
Root
    C
    C#/Db
    D
#   ...
    B
```

Some of these tags are very useful for finding material to feed granular synths with. If I want anything pitched, the Polyphony tag is often enough, or a specific Scale and Root if I'm doing it in the context of a song. I also use Root for setting a single note's pitch (useful with the One-Shot tag).

The Envelope tags roughly describe how volume changes over time, but most importantly, they define a sound's function in a song. You might recognize some of these names from preset categories in synthesizers, but some of them are more esoteric.

- Base: A kick-like sound, or anything that can be used as a (conventional or super weird) kick, even some foley can be categorized as Base
- Top: A snare/clap like sound
- Perif: Stands for "peripheral": tom-like sounds that can be used as secondary percussion. Again, a lot of foley and glitches go here
- Cym: Noisy, cymbal-like sounds: fast attack a relatively short decay
- Pad: Sustained, evolving sound with long attacks and decays
- Pulsation: Tremolo-like
- Pluck/Key: Fast attack and medium decay, but for pitched sounds
- Texture: No distinctive elements, can be easily used as a layer for other sounds
- Earcandy: Foley/designed sounds to use as filler

I might add tags for microtonal music, but it's not a priority currently.

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

## Gear Info

```yaml
Hardware
    Eurorack
    Guitar Pedal
    Analog
Digital
    Software
        Cardinal Synth
        Bespoke Synth
        Vitalium
        Surge XT
        SoundThread
        Cecilia
#       ...
Audio Effect
```

Gear used to make the sound.

## Synthesis/Processing Info

```yaml
Unprocessed
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

## License

```yaml
Creative Commons
    CC0
    CC-BY
Copyrighted
```

## Authorship

```yaml
Original
Derived
Downloaded
```

## Meta

```yaml
Wavetable
Impulse Response
Render
    Stem
    Track
```

These tags respond to a more "meta" version of the question "What is this sound?". It even opens the possibility of non-audio entries like presets or effect chains. I still need to work on that though.

Some clarifications:

- Render: Any piece of music that comes out of a DAW, finished or not
- Stem: Rendered group of instruments
- Track: Full song
