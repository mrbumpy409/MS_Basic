# MS Basic

MS Basic is a General MIDI-compatible SoundFont for virtual instrument playback in MuseScore Studio. It is based on the previous “MuseScore_General” SoundFont, which itself was based on “FluidR3” by Frank Wen. Detailed information on presets and sample sources used can be found in `Sample_Sources.csv`. All instruments without attribution are still using samples from FluidR3.

## Building

1. Install the following prerequisites:
   * [sfutils](https://github.com/bakajikara/sfutils)
   * [sftools](https://github.com/musescore/sftools) (optional, needed only for conversion to SF3)

2. Navigate one folder up from the GitHub source. So, for example, if the cloned GitHub repo is in `/home/user/source/MS_Basic`, then you want to navigate to `/home/user/source/`.

3. Run the following command:
   ```
   sfutils compile MS_Basic
   ```
   This will create `MS_Basic.sf2` in the current working directory.

4. To create a compressed SF3 version of the SoundFont (e.g., for distribution with MuseScore Studio), run:
   ```
   sf3convert -z -q 0.8 -a -1 MS_Basic.sf2 MS_Basic.sf3
   ```
   This sets OGG quality to 0.8 and adds 1 dB of dynamic headroom to avoid clipping during compression. It is not recommended to use higher OGG compression (lower values), as this has been shown to create buzzing loops and other audible anomalies in the instruments.

## SoundFont Compatibility

MS Basic makes full use of SoundFont 2.01 specification modulators (particularly in the newer instruments) and requires a player/sampler with robust support for the standard. The following SoundFont engines are known to accurately play this SoundFont:

* [BASSMIDI](https://www.un4seen.com/bass.html) (version 2.4.14.28 or later)
* [FluidSynth](https://www.fluidsynth.org/)
* [KQ Sampei](https://apps.apple.com/us/app/kq-sampei/id1626784865) (iOS)
* [MuseScore](https://musescore.org) – _**NOTE:** Due to recent synth engine changes in MuseScore Studio, compatibility needs to be re-tested._
* [Sobanth VSTi](https://blog.rosseaux.net/page/e5ca75d98990e33b31dadc78a8df1333/Sobanth)
* [SpessaSynth](https://spessasus.github.io/SpessaSynth/) (web app)

## Presets

### General MIDI Presets

MS Basic is compatible with the [General MIDI standard](https://en.wikipedia.org/wiki/General_MIDI) with some additional presets from the [Roland GS standard](https://en.wikipedia.org/wiki/Roland_GS).

### Fluid r3 Additional Drum Kits

Additional drum kits have been inherited from FluidR3, beyond the kits specified in the [Roland GS standard](https://en.wikipedia.org/wiki/Roland_GS). It is possible that some of these kits will be removed in the future when new drum samples are added.

### Instrument Variations

In addition to the General MIDI presets, further instrument variations can be found on banks 20 and above, utilizing identical preset numbers so that General MIDI preset fallback can occur if ever the instrument becomes no longer available on the higher bank number. In other words, if you have a track assigned to bank #40, preset #48 “Celli Fast”, then try to play it using a different General MIDI device or SoundFont, the preset will fall back to bank #0, preset #48 “Fast Strings” instead, and playback will at least sound somewhat correct.

### MuseScore Marching Percussion

The following marching percussion presets exist in the percussion bank (bank 128):
* 56: Marching Snare
* 57: OldMarchingBass
* 58: Marching Cymbals
* 59: Marching Bass
* 95: OldMarchingTenor
* 96: Marching Tenor

These presets are used for marching percussion support in MuseScore and do not conform to GM layout.

### Expressive Presets

MS Basic features expressive variants of all sustained presets, indicated by “Expr.” at the end of the preset name. The dynamics of these presets are controlled using MIDI Control Change #2 (CC2), allowing fluid crescendos and diminuendos while a note is being held. This makes for much more realistic expression of strings, brass, woodwinds, etc. Note velocity no longer controls dynamics in these presets, but in some instruments, velocity will have some effect on the speed of the note attack. In MuseScore, the default (and ideal) behavior is for expressive instruments to have their dynamics controlled by sending identical values to both CC2 and note velocity (the latter only during note-on, naturally).

The expressive presets exist on higher bank numbers but use the same preset number as their non-expressive defaults. You can see what bank numbers the expressive presets use in column #2 (“Expr. Bank #”) of the included `Sample_Sources.csv` file. The general rule is as follows:

* Bank 0 expressive presets are on Bank 17
* Bank 8 expressive presets are on Bank 18
* Bank 20-126 expressive presets are one bank higher (e.g., Bank 20 Expr. presets are on Bank 21)

### Dummy Presets

To maintain preset compatibility with the more elaborate ensemble strings presets in the original version of MS Basic, version 2.0.0 and above contains dummy presets that are duplicates of the similar instruments found on bank 0. For example, the full SoundFont has the following instruments assigned to preset #48, all on different banks (presets listed in bank#:preset# format):

- **000:048 - Strings Fast**
- **020:048 - Violins Fast**
- **025:048 - Violins2 Fast**
- **030:048 - Violas Fast**
- **040:048 - Celli Fast**
- **050:048 - Basses Fast**

In the HQ version of the SoundFont, each of these presets sounds distinct since they feature unique samples for each section, but in MS Basic >= 2.0.0, these presets on banks 20 and higher are mere duplicates of **000:048 - Strings Fast**, and only exist to avoid issues transitioning between the HQ and lighter versions of the SoundFont.

All dummy presets are indicated as such in the included `Sample_Sources.csv` file.

