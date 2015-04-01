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

Notice that each of the scale degrees is lowercase, Clojure does not change the quality of the scale degree based on capitalization and capitalized degrees with throw an `IllegalArgumentException`. 

To resolve these degrees into absolute pitches using `degrees->pitches`:

```clojure
(degrees->pitches scale-degrees :dorian :E3)
; => (52 54 55 57 59 61 62)
```