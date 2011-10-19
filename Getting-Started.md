OK, so we're assuming that you've already installed Overtone, started a REPL and have connected to an scsynth server. If not, these pages will help you:

* [[Installing Overtone]]
* [[Starting a REPL]]
* [[Connecting scsynth]]

First let's define a synth:

```clj
> (definst foo [] (saw 220))
```

Inst calls the synth macro which takes a synthesizer definition form.  It will compile this form
down to a SuperCollider synthdef, load it onto the synthesis server, and then
return a function that can be used to trigger the synth.  So we just created a
saw wave at 220 hz.

Be careful, this will
be at 100% volume!!!

```clj
> (foo) ; Call the function returned by our synth
4      ; returns a synth ID number
> (kill 4) ; kill the synth with ID 4
> (kill foo) ; or kill all instances of synth foo
```

Synth trigger functions return an ID that can be used to modify or kill
instances.

The `saw` function represents a [unit-generator](http://danielnouri.org/docs/SuperColliderHelp/UGens/UGens.html), or [ugen](http://danielnouri.org/docs/SuperColliderHelp/UGens/UGens.html) (sounds like "you jen").  These are the basic building blocks for creating synthesizers, and they can generate or process both audio and control signals.  Check the link for
descriptions of many ugens from the SC documentation.  Also, they all have doc
strings in Overtone.

```
> (doc saw)
-------------------------
overtone.live/saw
([freq])

  [freq 440.0]

  freq - Frequency in Hertz (control rate).

  Band limited sawtooth wave generator

  Categories: Generators -> Deterministic
  Rates: [ :ar ]
  Default rate: :ar
```

Insts can take arguments:

```clj
> (definst bar [freq 220] (saw freq))
> (bar 110)
5
> (kill bar)
```

you can also trigger multiple synths and kill them all with one kill command:

```clj
> (definst baz [freq 440] (* 0.3 (saw freq)))
> (baz 220)
> (baz 660)
> (kill baz) ; stop all running synths
```

Remember `(stop)`, as it can save you when accidentally trigger a bunch of
synths and you need to kill the audio fast.

```clj
> (foo)
> (bar)
> (baz)
> (stop) ; stop all running synths
```

When this synth is running the saw wave ugen is outputing an audio signal.  This
signal is represented as a continuous stream of floating point values between -1
and 1, so by multiplying by 0.3 we are just lowering the amplitude of this
signal, adjusting the volume.

We can change paramaters of the running synth on the fly with `ctl`

```clj
> (definst quux [freq 440] (* 0.3 (saw freq)))
> (quux)
> (ctl quux :freq 660)
```

So far we've just used a single ugen and passed it arguments, but ugens can be
plugged into each other in arbitrary ways too.  Basically anywhere a ugen takes
an argument value it can also take an input signal that will control that value.
Lets put a tremolo on our saw wave:

```clj
> (definst trem [freq 440 depth 10 rate 6 length 3]
    (* 0.3
       (line:kr 0 1 length FREE)
       (saw (+ freq (* depth (sin-osc:kr rate))))))
> (trem)
4
> (kill trem)
> (trem 200 60 0.8)
4
> (kill trem)
> (trem 60 30 0.2)
...
```
The `line` ugen outputs a value from the start value to the end value over a
specific length of time.  In this example we use it as a simple way to stop the
synth after a few seconds.  The last argument, `FREE`, is a typical argument to
this kind of control ugen that tells the ugen to free the whole synth instance
once it completes.  That way you don't have to `kill` it by hand anymore.

Also note that the line and sin oscillator ugens have the `:kr` suffix.  Many of
the ugens can operate at different rates, shown at the bottom of the doc string.
The two primary rates are audio rate and control rate, `:ar` and `:kr`.  Audio rate
runs at the rate of your audio card, and control rate runs at about 1/60 of that
speed, so for signals that are just controlling a value rather than outputting
audio you can save wasted CPU by using `:kr`.
