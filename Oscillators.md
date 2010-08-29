The oscillator ugens act as your source of raw audio content.  In subtractive synthesis, which we'll be focusing on here, you start by generating an audio signal with energy in the frequency bands you desire.  The typical wave forms come from the original analog synthesizers, where electronic circuits were used to generate periodic waveforms.  Take the sin wave, for example:

```clj
(defsynth sin-wave [attack 0.01 sustain 0.4 release 0.1 vol 0.4] 
  (* (env-gen (linen attack sustain release) 1 1 0 1 :free)
     (sin-osc freq)
     vol))

```
.  At the basic level you can think of any sound as being made up of a whole bunch of sine 