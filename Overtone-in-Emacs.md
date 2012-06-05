For the best live coding experience in emacs, you'll want to install...

* Leiningen 2
* Emacs Live
* lein-swank


##Leiningen 2
See https://github.com/technomancy/leiningen/wiki/Upgrading

    $ wget -O ~/bin/lein2 https://raw.github.com/technomancy/leiningen/preview/bin/lein
    $ chmod 755 ~/bin/lein2

## Emacs Live
See https://github.com/overtone/emacs-live#getting-started

    bash <(curl -fsSL https://raw.github.com/overtone/emacs-live/master/installer/install-emacs-live.sh)



## lein-swank

Create a file called `~/.lein/profiles.clj` with the following contents:
    {:user {:plugins [[lein-swank "1.4.4"]]}}


## Pulling it all together

* `cd` into a directory containing a lein project which references overtone as a dependency. 
* Fire up swank: `lein swank`
* Fire up Emacs
* Connect Emacs to swank: `M-x slime-connect <RET> <RET> <RET>`
* Fire up Overtone:

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
