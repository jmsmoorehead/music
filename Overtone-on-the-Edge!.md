If you'd like to be running the latest development version of Overtone, here's what you need to do.
This guide assumes that you are using lein, but cake works just fine too.

##Get the latest code from github.

```sh
$ git clone git://github.com/overtone/overtone.git
$ cd overtone
$ lein deps
```

##Launch a REPL
The quickest way to get started is to launch a clojure repl using lein. 
In the overtone project directory....

```sh
$ lein repl
```

Then make some noise :)

```clj
user> (use 'overtone.live)
   ...wait a bit...
user> (demo (sin-osc))
```

For a better experience try [Overtone in emacs](Overtone In Emacs).
