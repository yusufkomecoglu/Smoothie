# Smoothie

Smoothie is a spectral resonance suppressor for REAPER, written as a JSFX. It
follows the spectrum of the incoming audio (or a sidechain) and turns down
narrow, harsh resonances while leaving the overall tonal balance alone.

## Install

By hand:

- Download [`Dynamics/Smoothie.jsfx`](Dynamics/Smoothie.jsfx).
- Put it in `<REAPER resource path>/Effects/dynamics/`. Options → Show REAPER
  resource path in explorer/finder takes you to the right place.
- Restart REAPER (or rescan in the FX browser). It shows up as "JS: Smoothie".

## How to use

Put it on a track or item like any other FX. It processes channels 1-2; any
other channels pass through untouched. Supported sample rates are 44.1, 48,
88.2 and 96 kHz. At any other rate the audio passes through unprocessed.

The controls, by their names in REAPER's parameter list:

- **Depth** - overall amount of suppression.
- **Detail**, **Attack**, **Release** - how the detector tracks the signal.
  Each has a "tilt low" and "tilt high" partner so you can set it differently
  at the bottom and top of the spectrum.
- **Mode** - Soft or Hard suppression.
- **Quality** - Normal, High or Ultra. Higher settings analyse in smaller
  steps.
- **Low latency** / **Linear phase** - alternative filter modes (see latency
  below).
- **Stereo mode** (L/R or M/S), **Stereo link**, **Stereo focus**.
- **Bands** - up to eight bands that shape where and how hard Smoothie works:
  frequency, depth (-12 to +12), Q, slope, focus and shape (low cut, bell,
  high cut and a few variants). Each band can be enabled on its own, and
  **Band solo** lets you hear just that band's region. Drag the bands in the
  graph or use the sliders.
- **Max cut**, **Wet trim**, **Mix**, **Out trim**.
- **Delta** - outputs the difference between dry and processed, i.e. what is
  being taken out.
- **Bypass** - plays the dry signal, delayed to stay aligned with the
  processed one.

Clicking the "GR dB" label in the graph switches the gain-reduction scale
between 12, 18 and 24 dB.

## Sidechain

To drive the detector from another track, route that signal to input pins 3/4
and turn on **Sidechain**. With it off, the detector listens to the main input
and ignores pins 3/4.

**Sidechain listen** replaces the output with whatever is on pins 3/4 (it
doesn't care whether Sidechain is on), so you can check your routing before
using it. That signal is delayed by the plugin's latency so it lines up with
the processed audio. It overrides Band solo, Delta and Mix; Bypass overrides
it. If nothing is routed to pins 3/4 you'll hear silence.

## Latency

REAPER compensates for the delay automatically.

| Sample rate | Low latency | Default | Linear phase |
|---|---|---|---|
| 44.1 / 48 kHz | 0 | 2304 | 3456 |
| 88.2 / 96 kHz | 96 | 4704 | 7008 |

Figures are in samples. If both Low latency and Linear phase are on, Low
latency wins.

## Notes

Parameter changes are picked up once per audio block, not per sample.

## License

GPL-3.0-only. See [LICENSE](LICENSE).
