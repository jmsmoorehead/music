The oscillator ugens act as your source of raw audio content.  In subtractive synthesis, which we'll be focusing on here, you start by generating an audio signal with energy in the frequency bands you desire.  The typical wave forms come from the original analog synthesizers, where electronic circuits were used to generate periodic waveforms.  Here are some of the classic waveforms.  Experiment with different frequencies, attack, sustain and release settings too.  Many sounds will feel quite different depending on how you fade in and out of them.

```clj
(defsynth sin-wave [freq 440 attack 0.01 sustain 0.4 release 0.1 vol 0.4] 
  (* (env-gen (lin-env attack sustain release) 1 1 0 1 :free)
     (sin-osc freq)
     vol))
(sin-wave)
```

```clj
(defsynth saw-wave [freq 440 attack 0.01 sustain 0.4 release 0.1 vol 0.4] 
  (* (env-gen (lin-env attack sustain release) 1 1 0 1 :free)
     (saw freq)
     vol))

(defsynth square-wave [freq 440 attack 0.01 sustain 0.4 release 0.1 vol 0.4] 
  (* (env-gen (lin-env attack sustain release) 1 1 0 1 :free)
     (lf-pulse freq)
     vol))

(defsynth noisey [freq 440 attack 0.01 sustain 0.4 release 0.1 vol 0.4] 
  (* (env-gen (lin-env attack sustain release) 1 1 0 1 :free)
     (pink-noise) ; also have (white-noise) and others...
     vol))

(defsynth triangle-wave [freq 440 attack 0.01 sustain 0.1 release 0.4 vol 0.4] 
  (* (env-gen (lin-env attack sustain release) 1 1 0 1 :free)
     (lf-tri freq)
     vol))
```

Note that you can also use these generators as control signals to modify parameters of other ugens.  Here an adjustable width pulse wave is shifting the frequency of the main oscillator:

```clj
(defsynth spooky-house [freq 440 width 0.2 
                         attack 0.3 sustain 4 release 0.3 
                         vol 0.4] 
  (* (env-gen (lin-env attack sustain release) 1 1 0 1 :free)
     (sin-osc (+ freq (* 20 (lf-pulse:kr 0.5 0 width))))
     vol))
```