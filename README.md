# FV1 Programs for the Dual Defect 289

The "Dual Defect Processor" Model 289 is a Buchla-format modular synth module
that is based on the FV-1 from Spin Semiconductor. This repository contains
several sets of alternate DSP programs for this module, with a focus on
time-domain effects.

To use these programs, you will need some method of flashing the compiled builds
on to a suitable EPROM. Alternately, if you have the FV-1 development kit then
you may compile them from source and use the official development board to
program the EPROM.

Unlike many commercially available program sets, these algorithms are made
available under the MIT License and are free for commercial or personal use.

The reverb algorithms presented here are common in academic literature,
but novel in terms of what is available in the public domain today for the FV-1.
I welcome any discussion around the utility of these algorithms and further
feedback on tuning and refining them.

## Programs

The 289 is composed of two identical sections. The upper and lower sections can
load distinct sets of 8 programs. The Cambridge programs are intended to be
loaded into the top section, and the Boston programs into the lower. There are
a number of use cases where the programs can interoperate.

### Cambridge Programs

The Cambridge programs are a diverse set of delay and stereo-widening effects.
They are based on multi-tap delay lines which are scaled or modulated
differently in each program to achieve different effects.

| D | # | Program       |  Description  |
|---|---|---------------|---------------|
| 1 | 7 | Long Delay    |  Mono 1s delay. Summed mono input. Separate left and right taps. |
| 2 | 3 | Long Chorus   |  Mono 1s delay. Summed mono input. Chorus on both taps.  |
| 3 | 5 | Stereo Delay   |  Stereo 500ms delay.  |
| 4 | 1 | Dimension             | Stereo multi-chorus.      |
| 5 | 6 | Reflections (Small)   | Stereo early reflections, small space.   |
| 6 | 2 | Reflections (Medium)  | Stereo early reflections, medium space.  |
| 7 | 4 | Reflections (Large)   | Stereo early reflections, large space.   |
| 8 | 0 | Mobius Verb   | Mono reverb. Left is signal, right is feedback.  |

### Boston Programs

The Boston programs are reverbs that are based on an 8x8 Feedback Delay
Network (FDN). The programs are named for the aspect of the algorithm that can
be modulated in each.

| D | # |Program       |  Description  |
|---|---|------------|---------------|
| 1 | 7 | Long Delay        | Mono 1s delay. Summed mono input. Separate left and right taps. |
| 2 | 3 | Darkness (medium) | Stereo reverb with variable input low pass filters. |
| 3 | 5 | Darkness (large)  | Stereo reverb with variable input low pass filters. |
| 4 | 1 | Distance (large)  | Stereo reverb with variable distance from source.   |
| 5 | 6 | Chorus   (medium) | Stereo reverb with variable chorus modulation.      |
| 6 | 2 | Time     (medium) | Stereo reverb with variable delay size/time.        |
| 7 | 4 | Time     (large)  | Stereo reverb with variable delay size/time.        |
| 8 | 0 | Mobius Verb       | Mono reverb. Left is signal, right is feedback.     |

Note that the 289 program selection is not the same ordering as the EPROM

  *  The `#` column indicates the program position on the EPROM.
  *  The `D` column indicates the algorithm position on the 289 panel.

### Cooperative Patches

The two sets of programs are designed to interoperate in useful ways when patched
together. Here are a few ideas:

1.  The Long Delay is the first program in both sets. Alone it is a 1 second,
    two tap delay. Patched together it is a 2 second 4 tap delay, or a really
    long pre-delay for a reverb. Remember you can always insert additional
    analog processors like filters between them or in feedback paths.

2.  Try Reflections on top, blended with the dry, and then patched to a reverb
    below, also blended again. A large number of flexible, naturalistic reverbs
    are possible this way.

3. The Mobius Verb is the last program in both sets. Try it as a stereo reverb,
   using each section for left and right individually. The right output is
   feedback that can be cross-patched between the two sections.
