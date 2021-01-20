## "Cambridge" Stereo Early Reflections Algorithm

This is a true stereo multi-tap algorithm with some diffusion that creates
the early reflections part of a reverb.

It looks like this:

Left Input -> Low pass -> Variable pre-delay -> Peak limiter ->
  4 Taps -> All pass diffuser -> 4 Taps -> All pass diffuser -> 4 Taps -> Out L

Right Input -> Low pass -> Variable pre-delay -> Peak limiter ->
  4 Taps -> All pass diffuser -> 4 Taps -> All pass diffuser -> 4 Taps -> Out R

Within each set of four taps, there is one that reads from the alternate channel.
Each tap is scaled down slightly so that the sound decays naturally.

The two all pass diffusers are modulated with sine LFOs, which gives a gentle
chorusing sound to the more distant taps.

### Controls

Pot 0 controls the left pre-delay length. This control may be smoothly modulated
with the expected pitch warble.

Pot 1 controls the right pre-delay length. This control may be smoothly modulated
with the expected pitch warble.

Pot 2 controls the decay of the taps. At minimum, the taps decay quickly
and the reflections are more naturalistic. At maximum, all of the taps are almost
the same volume and the effect is more dramatic. If feedback is used, unpleasant
runaway oscillation is likely at higher settings.
