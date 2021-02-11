## Notes for Reverb Nerds

When beginning to learn about reverb topologies I found useful information
challenging to come by and so I think it's important to document how and why
one's programs work as part of placing them in the public domain.

### Background

The reverb programs here are based on feedback delay network (FDN) topologies.
This is a well known concept that is documented and explored in a lot of academic
literature, and has been used commercially at least as far back as the mid 1980s.
I won't retread the theory and principles of FDNs as they are well described
elsewhere. In short, some number of delay lines are fed back on to each other
in a pattern that maximizes the number of echoes until it approximates a
naturalistic reverberation. There are a lot of details between that concept and
getting them to sound good.

FDNs in general exist in an alternate universe to the other common reverb topology
which is known as an allpass loop. An allpass loop topology uses a single loop of
delays and diffusers built from allpass filters to diffuse the sound. Allpass loops
are well represented in publicly available FV-1 programs as the chip's inventor,
Keith Barr (of Alesis fame) was a big proponent of them and the part is optimized
in many ways to make these types of reverbs easily.

#### FDN Basics

FDNs are usually sized in powers of two, with 4x4, 8x8, and 16x16 being the most
common sizes that I see described in the literature.

The Boston programs use an 8x8 FDN. This is a larger network than other
FV-1 programs that I know of. It is a challenge to fit it into the limitations of
the FV-1 chip (1 second of delay time and 128 instructions per tick). A few
optimizations were needed and shortcuts were taken to make this work.

The Cambridge programs use a 3x3 FDN and create a much simpler scattering
pattern that is more appropriate for specular early reflections. However, even
this size network sounds sort of like a bad reverb if the feedback is turned up
high enough.

Here are a few basic things that I have learned about FDNs along the way that
will help you to understand why these programs are structured the way they are.

1.  Like all reverb topologies, the choice of delay sizes matters a lot.
    These programs use delay sizes mostly in the 1k-4k (samples) range,
    with larger or shorter delay lines for special effects.

2.  There is a sort of superstition in reverb subculture about using prime numbers
    for delay times which dates to the very earliest research in the field.
    This matters (a lot) for "parallel combs" style topologies, but appears to
    be significantly less important for FDNs. The delay paths in an FDN are much
    more complex, and so there are many non-prime delay sizes that work just as well.

3.  The feedback matrix must be _orthogonal_ if you want to be able to support
    very long decay times. This means that the total energy in the system is
    preserved by the feedback matrix unless losses are deliberately introduced.
    In practice, this means you can turn the decay time up to (almost) infinity.
    When you are working on a reverb that is supposed to be infinite, you can
    easily check if you have a bug in your algorithm by turning the feedback gain
    to exactly 1 and seeing if the sound decays or grows out of control.

4.  The 8x8 feedback matrix that I have used is very common in FDNs.
    It's called a _Hadamard_ matrix, and it looks like this.
    The `+` is 0.35355 and the `-` is -0.35355 (1 over square root of 8).

    ```
    1  + + + + + + + +
    2  + - + - + - + -
    3  + + - - + + - -
    4  + - - + + - - +
    5  + + + + - - - -
    6  + - + - - + - +
    7  + + - - - - + +
    8  + - - + - + + -
    ```

5.  A naive implementation of any feedback matrix is always at least O(n^2)
    complexity, which means it will require at least 64 multiplications to
    calculate. In our case, each feedback requires 8 scaled delay reads,
    (the adds and multiplies are free which is cool) and 1 delay write, so 9
    total FV-1 opcodes. This means that just the feedback for the the 8x8 matrix
    would require 72 of our 128 instructions, which doesn't leave enough space
    to build a useful program.

6. There is an optimization (Fast Walsh-Hadamard) where we recognize that the
   8x8 Hadamard matrix is composed of similar 4x4 matrices and the 4x4 is made of
   similar 2x2s etc. In practice, we calculate 8 distinct 1x4 matrices and combine
   them in eight different ways, which ends up saving just enough instructions
   to squeeze in the other features. Phew! That optimized matrix looks like this:

   ```
   1a  1b
   2a  2b
   3a  3b
   4a  4b
   1a -1b
   2a -2b
   3a -3b
   4a -4b
   ```

7. FDNs must include loss factors in the feedback so that the reverb actually
   decays. One of the most useful ways to do this is with low pass filters,
   which approximates the way reflected sound in a room naturally loses high
   end energy faster than lows. In most of these programs, a 1 pole low pass
   filter is placed in the feedback path of each delay line. In some programs,
   we run out of space for the filters due to the inclusion of other features,
   and so they were omitted.

#### Stereo Reverbs

True stereo reverbs are a powerful mixing tool, as they let you use your pan
pots naturally, and still maintain a somewhat realistic stereo image. When a sound
is panned to one side, most of the early reverb energy will appear at that side,
and gradually appear on the other, and then eventually it all mixes together if the
decay time is substantial. The Boston programs are all stereo reverbs.

We do this by splitting the 8x8 FDN into two conceptually, with the first four
delay lines representing the left side and the second four the right. The dry
input signal is injected into only one half of the delay lines, and the feedback
within the matrix is what spreads the energy around. I have followed a convention
of tapping the fourth and eighth delay lines for most of the output, which seems
to produce a reasonable stereo image.

These output taps sort of model the distance from the listener to the source.
As one varies the position of the output tap, the effect is that the source
seems to approach or recede into the reverberant space of the room.
The "Distance" program is based on this idea.

#### Early reflections

Most full reverb programs combine a late reverberation structure with an early
reflections model. Managing early reflection energy is a really interesting thing
to explore when mixing a lot of different sources together, especially if your
goal is to make them all appear to be together in the same space. The Cambridge
programs are my attempt to make an early reflections algorithm that is a flexible,
usable mixing tool.

The algorithm is pretty simple: left and right sources are input limited to
soften their dynamics, low pass filtered, and then scattered in a small 3x3 FDN.
Six taps are read out of each side of the FDN, summed in a way so that they decay
naturally, and passed through a few gentle all pass diffusers.

The tap times that were chosen are essentially random. My conclusion was that
there is no particular arrangement of taps that is any more magically useful than
any other, unless some very specific special effect is desired.
