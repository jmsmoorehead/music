If you'd like to be running the latest development version of Overtone, here's what you need to do.
This guide assumes that you are using lein, but cake works just fine too.

#Installation
##Install Seesaw
Overtone uses Seesaw to make working with Swing in Clojure more fun! you'll need the latest version of Seesaw to take advantage of Overtone's new gui widgets.

See (https://github.com/daveray/seesaw).

```sh
$ git clone https://github.com/daveray/seesaw.git
$ cd seesaw
$ lein deps
$ lein install
$ cd ..
```

##Install Overtone
Get the latest code from github.

```sh
$ git clone git://github.com/overtone/overtone.git
$ cd overtone
$ lein deps
```

#REPL Quick Start
The quickest way to get started is to launch a clojure repl the overtone project directory using lein.
```sh
$ lein repl
```

Then make some noise :)
```clj
user> (use 'overtone.live)
   ...wait a bit...
user> (demo (sin-osc))
```

#Resources
* [Overtone in emacs](Overtone In Emacs)
