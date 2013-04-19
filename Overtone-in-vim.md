## Installation

For the best live coding experience in vim, you'll want to install:

* [vim-clojure-static](https://github.com/guns/vim-clojure-static)
* [vim-fireplace](https://github.com/tpope/vim-fireplace)
* [vim-classpath](https://github.com/tpope/vim-classpath)

Some tips:

* The first time you open a Clojure file, it'll take a few seconds for the Java VM to load
* Within a Clojure file, you can use `cpp` to evaluate the inner-most expression at the cursor, or `:Require` to reload the whole file.