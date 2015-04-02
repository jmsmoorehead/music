From the Clojure REPL you can access some built-in examples of Overtone code by calling the `examples` function.

```clojure
(examples)
```

This will print out a series of examples that you can play with. Here is one of them:

```
dbrown
  :rand-walk       (:ar) - Random floating point
                           number walk through
                           freqs with rate
                           determined by mouse-x
```

If you want to test them out, use the `demo` function:

```clojure
; Plays a short demo, move your mouse!
(demo (example dbrown :rand-walk))

; You can play the demo for longer by passing in a time argument in seconds
(demo 10 (example dbrown :rand-walk))
```