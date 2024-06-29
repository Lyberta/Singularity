# Free and Equal Against All Odds

## Description

A piece that is a direct inspiration and response to United Nations Free And Equal 2014 video ["The Power Of Sharing"](https://www.youtube.com/watch?v=0O03jJ6JTyU).

I'm speaking up in a way that I can - via music.

## Instrumentation

* Piano
* 1st Violins
* 2nd Violins
* Violas
* Cellos
* Trumpet
* French Horns
* Piccolo
* Electric Bass
* Drumkit

## Basic info

* Key: G minor
* Tempo: 80 bpm
* Time signature: 4/4

## Render setup

* Sequencer: Rosegarden
* Sampler: LinuxSampler
* Samples: Salamander Grand Piano, Sonatina Symphonic Orchestra, Flame Studios Collection, Salamander Drumkit
* Reverb: Calf Studio Gear

### Files

* `Free_and_Equal_Against_All_Odds.rg` - Rosegarden project file holding all the MIDI data.
* `Free_and_Equal_Against_All_Odds.lscp` - LinuxSampler instruments.
* `Free_and_Equal_Against_All_Odds.calf` - Calf Studio Gear effects.
* `Free_and_Equal_Against_All_Odds.mscz` - MuseScore 3 sheets for live performance by a real orchestra.

### Connections

### MIDI

* Rosegarden output named "out 1 - General MIDI Device" goes into LinuxSampler.

### Audio

* LinuxSampler output named "Piano" goes into "reverb".
* LinuxSampler output named "LinuxSampler" goes into "reverb2".
* Both reverbs go into Rosegarden inputs named "record in" for bouncing.
* Both reverbs go into any kind of hardware output for live monitoring.
