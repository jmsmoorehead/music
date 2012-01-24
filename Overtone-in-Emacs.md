For the best live coding experience in emacs, you'll wan't to install...

* swank-clojure
* live-coding-emacs

##swank-clojure
See (https://github.com/technomancy/swank-clojure).

```sh
$ lein plugin install swank-clojure 1.3.4
$ cd overtone
$ lein swank
```

##live-coding-emacs config
See (https://github.com/overtone/live-coding-emacs).

```sh
$ cd ~/
$ git clone https://github.com/overtone/live-coding-emacs.git
$ mv .emacs.d/ .emacs.d.old
$ mv live-coding-emacs/ .emacs.d/
```

Launch emacs and type `M-x slime-connect <RET> <RET> <RET>`

##Hello World!

```clj
user> (use 'overtone.live)
          _____                 __
         / __  /_  _____  _____/ /_____  ____  ___
        / / / / | / / _ \/ ___/ __/ __ \/ __ \/ _ \
       / /_/ /| |/ /  __/ /  / /_/ /_/ / / / /  __/
       \____/ |___/\___/_/   \__/\____/_/ /_/\___/

                          Programmable Music. v0.7-dev


Hello User, may this be the start of a beautiful music hacking session...
nil
user> (demo (sin-osc))

```
