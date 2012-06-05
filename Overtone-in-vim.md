## Installation
For the best live coding experience in vim, you'll want to install...

* vimclojure
* nailgun (optional)

A great way to get started with vimclojure in vim is Dave Ray's [vimclojure-easy](https://github.com/daveray/vimclojure-easy).

## Getting started

### Plain 'ole repl

 * Start editing a song.clj file in vim
 * Use the Overtone live namespace: `(ns your.song (:use [overtone.live]))`
 * Start a Clojure repl e.g. `lein repl`
 * `(use 'your.song)`
 * You can now start executing bits of music defined in your.song!

### Nailgun

 * Start the nailgun server (see vimclojure-easy for instructions)
 * Start editing a song.clj file in vim
 * Use the Overtone live namespace: `(ns your.song (:use [overtone.live]))`
 * Evaluate the file (`\ef`)
 * You can now start evaluating lines (`\el`) and forms (`\ep`) interactively with vimclojure!