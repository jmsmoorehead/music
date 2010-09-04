Overtone comes with the midi-clj library which provides a no nonsense interface to the built-in Java midi support.  Calling either `(midi-in)` or `(midi-out)` with no arguments will bring up a list of all available midi input or output devices.  After clicking on a device the function will return with a handler that can be used to communicate with the device.  Once you know the name of your midi device you can pass a search string that will then return the first matching device.  This grabs an Axiom66 usb-midi keyboard:

```clj
(def kb (midi-in "axiom"))
```

To register a callback function to receive midi events from an input device just pass the device and function to `midi-handle-events`:

```clj

; define a synth to play with the midi keyboard
(defsynth foo [note 60 vel 0.8]
  (let [freq (midicps note)]
    (* vel
       (env-gen (perc 0.01 0.2) 1 1 0 1)
       (+ (sin-osc (/ freq 2))
           (rlpf (saw freq) (* 1.1 freq) 0.4)))))

; Play the note with the specified velocity, converted from midi range to synth range (0-128 => 0-1.0)
(defn midi-player [event ts]
  (foo (:note event) (/ (:vel event) 128.0)))

(midi-handle-events kb #'midi-player)
```

To output midi you can send events directly to a device:

```clj

; Using a software virtual midi driver you can route midi from one program to another
(def ableton (midi-out))

; Trigger midi note 60 with a velocity of 100
(midi-note-on ableton 60 100)

; Now stop the note
(midi-note-off ableton 60)
```
