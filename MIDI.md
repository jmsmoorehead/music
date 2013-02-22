## Using the event stream

Overtone 0.7.1 automatically detects all connected MIDI devices on boot and registers the appropriate handlers for you. To see a list of MIDI devices detected by Overtone, use:

```clj
(connected-midi-devices)
```

The MIDI device should be connected and powered on before starting Overtone. When you bash the keys on the keyboard, Overtone receives internal events in its event stream. To see them use:

```clj
(event-debug-on)
```

To stop:

```clj
(event-debug-off)
```

You should see that for each key press, there are two events. A general midi control change event:

```clj
[:midi :note-on]
```

and a device-specific event i.e.:

```clj
[:midi-device Evolution Electronics Ltd. Keystation 61e Keystation 61e :note-on]
```

For simplicity use the general event type:

```clj
(on-event [:midi :note-on]
          (fn [e]
            (let [note (:note e)
                  vel  (:velocity e)]
              (your-instr note vel)))
          ::keyboard-handler)
```

The last argument is a keyword which can be used to refer to this handler, so you can later do:

```clj
(remove-handler ::keyboard-handler)
```

## Using midi-clj directly

Overtone comes with the midi-clj library which provides a no nonsense interface to the built-in Java midi support.  Calling either `(midi-in)` or `(midi-out)` with no arguments will bring up a list of all available midi input or output devices.  After clicking on a device the function will return with a handler that can be used to communicate with the device.  Once you know the name of your midi device you can pass a search string that will then return the first matching device.  This grabs an Axiom66 usb-midi keyboard:

```clj
(def kb (midi-in "axiom"))
```

To register a callback function to receive midi events from an input device just pass the device and function to `midi-handle-events`:

```clj

; define an inst to play with the midi keyboard
(definst foo [note 60 vel 0.8]
  (let [freq (midicps note)]
    (* vel
       (env-gen (perc 0.01 0.2) 1 1 0 1 :action FREE)
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