## Manual

Controls correspond to the panel legend on the 289.
Latest info always available at https://github.com/wir35/dual-defect-289

  * 01 - Cambridge - New Delay
  * 02 - Cambridge - Dimension
  * 03 - Cambridge - Reflections (Medium)
  * 04 - Boston - Width
  * 05 - Boston - Darkness (Medium)
  * 06 - Boston - Time (Large)
  * 07 - Waltham - Diffuse (Medium)
  * 08 - Waltham - Far (Medium)

#### 01 New Delay

A 1 second mono delay with two output taps. The tap times are quantized to
increasing powers of two, to facilitate rhythmic effects. Use the time base
knob to fine tune the delay times. The Z control introduces a micro shift between
the two taps for wider stereo effects.

| Control | Usage |
|-------|------------------------------------
| Ins   | Inputs summed to mono. |
| Outs  | Left is tap 1. Right is tap 2. |
| X     | Tap 1 time. |
| Y     | Tap 2 time. |
| Z     | Tap 1 and 2 microshift time. |
| Time  | Extends delay time. Reduces bandwidth. |
| Regen | Use regen knobs to get echo feedback from 1 or 2. |
| Bal   | Mix dry and wet signals. |

#### 02 Dimension

This is a gentle chorus to add stereo dimension/width to any sound. The signal
passes through a crossover and the high and low frequencies have distinct choruses.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo input. |
| Outs  | Stereo output. |
| X     | Micro delay between left and right channels. |
| Y     | Modulation speed. |
| Z     | Modulation depth. |
| Time  | Extends delay times. Slows LFOs. Reduces bandwidth. |
| Regen | Not recommended. |
| Bal   | Use 100% wet. |

#### 03 Reflections (Medium)

Stereo early reflections program modeling a medium sized space. Use the balance to
blend with the original signal and then cascade it to the reverbs in the lower section.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo input. |
| Outs  | Stereo output. |
| X     | Reflections decay time. |
| Y     | Left predelay time. |
| Z     | Right predelay time. |
| Time  | Increases size. Decreases bandwidth. |
| Regen | Not recommended. Use X. |
| Bal   | Mix dry and wet signals. |

#### 04 Width

A very usable ambience style reverb, which can be used to add stereo width
and ambience to any source. Stereo input and stereo output. The Y control adjusts
the perceived width, adding early reflections and presenting a more
decorrelated stereo field. The Z control adjusts the perceived size of the room.
While extreme settings of X and Z together produce a long tail, this one is
optimized for shorter ambiences.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo input. |
| Outs  | Stereo output. |
| X     | Reverb decay time. |
| Y     | Stero width and modulation. |
| Z     | Room size. |
| Time  | Increases size. Decreases bandwidth. |
| Regen | Not recommended. Use X. |
| Bal   | Mix dry and wet signals. |

#### 05 Darkness (Medium)

Medium sized, true-stereo reverb with modulation of low pass filters on input.
Turn down Z for a very dark reverb, or all the way to gate input signal.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo inputs. |
| Outs  | Stereo outputs. |
| X     | Reverb time. |
| Y     | Unused. |
| Z     | Low pass filter cutoff.  |
| Time  | Increases size. Decreases bandwidth. |
| Regen | Not recommended. Howling. |
| Bal   | Blend dry and wet signals if desired. |

#### 06 Time (Large)

The time programs can be delays, reverbs or any combination in between.
An imbalanced FDN has several short delay lines and two long.
The time of the long delays can be modulated from short (reverb-like) to
long (echo-like). Reverb time controls the regeneration of both long and
short delays. Heavy modulation of delay time will dump time-warped,
deranged warble into the reverb network.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo inputs. |
| Outs  | Stereo outputs. |
| X     | Reverb time. |
| Y     | Delay time, left side. |
| Z     | Delay time, right side. |
| Time  | Increases delay time. Decreases bandwidth. |
| Regen | Not recommended, but maybe OK with low X. |
| Bal   | Blend dry and wet signals if desired. |

#### 07 Diffuse (Medium)

Concert hall algorithm with high internal diffusion. Creates a very
full and thick reverberation that builds slowly in density. The tone control is
bassy when low and bright when high. This also affects the reverberation time so
that lower or higher frequencies dwell longer. This program uses sizes close to
the original algorithm.

This program allows very deep, random modulation of the internal diffusors.
Keep the modulation depth at lower settings for more naturalistic reverb,
or high for special effects.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo input. |
| Outs  | Stereo output. |
| X     | Reverberation time. |
| Y     | Tone control. |
| Z     | Modulation depth. |
| Time  | Extends reverb time and size. Reduces bandwidth. |
| Regen | Not recommended. |
| Bal   | Mix dry and wet signals. |

#### 08 Far (Medium)

Concert hall algorithm with high internal diffusion. The listen distance
in this program is set very far so that the source appears much further away
than in the other programs.

Same tone control and modulation as the other programs.

| Control | Usage |
|-------|------------------------------------
| Ins   | Stereo input. |
| Outs  | Stereo output. |
| X     | Reverberation time. |
| Y     | Tone control. |
| Z     | Modulation depth. |
| Time  | Extends reverb time and size. Reduces bandwidth. |
| Regen | Not recommended. |
| Bal   | Mix dry and wet signals. |
