## Installation

For the best live coding experience in vim, you'll want to install:

* [vim-clojure-static](https://github.com/guns/vim-clojure-static)
* [vim-fireplace](https://github.com/tpope/vim-fireplace)
* [vim-classpath](https://github.com/tpope/vim-classpath)

Now:

* In one shell session, start a REPL using `lein repl`
* In vim, start writing your Overtone file
* The first time you want to hear some output, use `:Require` to reload the whole file
* After the file has been loaded once, use `cpp` to evaluate the inner-most expression at the cursor
* If you have problems, try reloading the entire file and dependencies with `:Require!`