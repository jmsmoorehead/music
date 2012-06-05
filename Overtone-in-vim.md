## Installation
For the best live coding experience in vim, you'll want to install...

* vimclojure
* nailgun

A great way to get started with vimclojure in vim is Dave Ray's [vimclojure-easy](https://github.com/daveray/vimclojure-easy).

## Getting started

 * Start the nailgun server (see vimclojure-easy for instructions)
 * Start editing a song.clj file in vim
 * Use the Overtone live namespace: `(ns your.song (:use [overtone.live]))`
 * Evaluate the file (`\ef`), which will take a while as it needs to start Supercollider.
 * You can now start evaluating lines (`\el`) and forms (`\ep`) interactively with vimclojure!