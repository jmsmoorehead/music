## Installation

For the best live coding experience in vim, you'll want to install:

* [vim-clojure-static](https://github.com/guns/vim-clojure-static)
* [vim-fireplace](https://github.com/tpope/vim-fireplace)
* [vim-classpath](https://github.com/tpope/vim-classpath)

Now:

* In one shell session, start a REPL using `lein repl`. It is important to do this as otherwise when you require your file for the first time, Overtone opens and blocks vim.
* In vim, start writing your Overtone file. Hint: it tends to work better if you use `overtone.live` rather than `overtone.core`.
* The first time you want to hear some output, use `:Require` to reload the whole file. You will also need to do this any time you add a new instrument or something else.
* After the file has been loaded once, use `cpp` to evaluate the inner-most expression at the cursor.
* You can also evaluate a single line with `:Eval` (in normal mode), or select multiple lines and run `:Eval` to run all of them.
* If you have problems, try reloading the entire file and dependencies with `:Require!` (note: this may take a few seconds).
* For more info, `:help fireplace`.