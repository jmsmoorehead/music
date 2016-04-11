# Overtone 0.9.1

See [the end of the midi/keyboard example](https://github.com/overtone/overtone/blob/master/src/overtone/examples/midi/keyboard.clj#L49-L64).


# Overtone 0.7.1

## Using the event stream

Overtone 0.7.1 automatically detects all connected MIDI devices on boot and registers the appropriate handlers for you. To see a list of MIDI devices detected by Overtone, use:

```clj
(midi-connected-devices)
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
(remove-event-handler ::keyboard-handler)
```

Apart from the ```:note-on``` events, there are also many more which can be found over here: 
https://github.com/overtone/midi-clj/blob/master/src/overtone/midi.clj#L167-191

Tables 1 and 3 would be very useful if you want greater control over overtone using midi.

http://www.midi.org/techspecs/midimessages.php
http://www.midi.org/techspecs/midimessages.php#3

Here's an example of checking if the sustain pedal is pressed:

```clj
(def sustain-pedal (atom false))

(on-event [:midi :control-change]
          (fn [e]
              (let [control-number (:data1 e)
                    value (:data2 e)]
                   (if (= control-number 64)
                       (when (or (and (>= value 64) (not @sustain-pedal)
                                 (and (<= value 63) ))
                             (swap! sustain-pedal #(not %)))
                       ;else
                       (when (and (<= value 63) @sustain-pedal)
                             (swap! sustain-pedal #))
              ))
           ::sus-pedal-handler)
```

## Sending MIDI messages

It is also possible to send MIDI messages to a receiver (Why not make the computer a jamming buddy :wink:)

```clj
(let [receiver (first (midi-connected-receivers))]
  ;Play a midi note c4 at 80 velocity for 1 second on the fourth channel
  ;Note that the channel is zero-indexed, whereas normal mixers/midi devices start counting them from 1.
  (overtone.midi/midi-note receiver (note :c4) 80 1 3)
  
  ;Turn on the sustain pedal to full on the first channel
  ;64 is the midi control number for the sustain (damper) pedal.
  (overtone.midi/midi-control receiver 64 127 0)
)

```

## Simple Midi Keyboard Control

Use `midi-poly-player` for simple control of Overtone instruments.

Define an inst to play with the midi keyboard

```clj
(definst steel-drum [note 60 amp 0.8]
  (let [freq (midicps note)]
    (* amp
       (env-gen (perc 0.01 0.2) 1 1 0 1 :action FREE)
       (+ (sin-osc (/ freq 2))
          (rlpf (saw freq) (* 1.1 freq) 0.4)))))
```

Define a player that connects midi input to that instrument.

```clj
(def player (midi-poly-player steel-drum))
```

When you want to stop or change sounds, use `midi-player-stop`.

```clj
(midi-player-stop)
```