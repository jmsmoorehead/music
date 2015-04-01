Overtone is capable further abstraction of pitches through [scale degrees](https://en.wikipedia.org/wiki/Degree_%28music%29), which is a way of referring to pitches within a scale. Scale degrees are commonly notated using roman numerals (I, IV, vii, etc.), so in Clojure scale degrees are referenced with keywords as shown below:

```clojure
(def scale-degrees [:I :ii :iii :IV :V :vi :vii])
```

To resolve these degrees into absolute pitches using `degrees->pitches`:

```clojure
(def scale-pitches (degrees->pitches scale-degrees :major :C3))
```

The available scales are quite large, which includes the common major/minor, modes (dorian, mixolydian, etc.), and more exotic scales. You can see the full list by running the following command in your REPL:

```clojure
(source SCALE)
```