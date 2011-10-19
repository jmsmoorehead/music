Once you've made it through the process of [[Installing Overtone]] you'll want to start a REPL so that you can start giving it music-making instructions.

For those not aware of the term REPL, it stands for Read Evaluate Print Loop and dates back to the early days of Lisps. Other languages call it the console or an interactive session or a prompt. Essentially it gives you a way to communicate live with Overtone so you can make it do your bidding and control it in real time - at least as fast as you can type!

You'll know when you've entered a REPL session because the terminal prompt will change from something like `$` to `user=>`. You can then enter Clojure forms as text and press return to execute it.

### Firing up a REPL

Exactly how to do this depends on which dependency management tool you used: [cake](http://clojure-cake.org/), [leiningen](http://github.com/technomancy/leiningen) or [maven](http://maven.apache.org/). All instructions require you to have the working directory of your terminal set to your project directory (i.e. `tutorial`). Once you see the `user=>` prompt, try typing the Clojure form `(+ 1 2)` to evaluate and return the answer `3`. This is the REPL in full action:

* READ - Clojure reads the form `(+ 1 2)` as text
* EVALUATE - Clojure does the sum `1 + 2` and resolves it to `3`
* PRINT - Clojure then prints the answer out to the screen
* LOOP - Clojure writes the prompt `user=>` again and patiently waits for another command to read.

#### Cake
```sh
$ cake repl
user=>(+ 1 2)
3
user=>
```

#### Lein
```sh
$ lein repl
user=>(+ 1 2)
3
user=>
```

#### Maven
Maven wizards - please fill me.

### What next?

Learn how to [[Connect scsynth|Connecting scsynth]] then head over to [[Getting Started]] to learn how to make some crazy sounds.

    

