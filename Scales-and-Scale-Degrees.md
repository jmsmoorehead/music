[Scales](https://en.wikipedia.org/wiki/Scale_%28music%29) can be quickly generated using the `scale` function, which takes a root note and the type of scale as arguments.

```clojure
(scale :C3 :major)
; => (48 50 52 53 55 57 59 60)
```

The available scales are quite large, which includes the common major/minor, modes (dorian, mixolydian, etc.), and more exotic scales. You can see the full list by running the following command in your REPL:

```clojure
(source SCALE)
```

Overtone is also capable further abstraction of pitches through [scale degrees](https://en.wikipedia.org/wiki/Degree_%28music%29), which is a way of referring to pitches within a scale. Scale degrees are commonly notated using roman numerals (I, IV, vii, etc.), so in Clojure scale degrees are referenced with keywords as shown below:

```clojure
(def scale-degrees [:i :ii :iii :iv :v :vi :vii])
```

Notice that each of the scale degrees is lowercase; Overtone does not change the quality of the scale degree based on capitalization. Capitalized degrees will throw an `IllegalArgumentException`.

You can resolve scale degrees into absolute pitches using `degrees->pitches`:

```clojure
(degrees->pitches scale-degrees :dorian :E3)
; => (52 54 55 57 59 61 62)
```

Scale degrees can be augmented by either `+` or `-` to denote the octave above or below the root of the scale, and can be sharped or flatted using `#` or `b`. For example in a major scale starting from C3 (MIDI pitch number 48), the scale degree `:ib+` would be resolved to a Cb4 (MIDI pitch number 59).

Another useful feature of scale degrees in Overtone is the `:_` keyword, which you can use to denote rests. Below is an example that uses both note ornament and the `:_` nil value:

```clojure
(def scale-degrees [:vi :vii :i+ :_ :vii :_ :i+ :vii :vi :_ :vii :_])
(def pitches (degrees->pitches scale-degrees :dorian :C4))

(defn play [time notes sep]
  (let [note (first notes)]
    (when note
      (at time (saw (midi->hz note))))
    (let [next-time (+ time sep)]
      (apply-at next-time play [next-time (rest notes) sep]))))
```