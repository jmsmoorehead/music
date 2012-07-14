Installing Overtone can be trivial or complex depending on your previous experience with Clojure projects, desire to use an external SuperCollider server and target OS. Here we'll walk you through all the steps assuming you have little or no prior Clojure knowledge.

Essentially, installation consists of the following steps:

* Perform any necessary OS-specific setup
* Create a new directory for your audio project
* Download the appropriate dependencies
* Download and install SuperCollider (if you wish to use an external server)

### OS-specific setup

* __Linux__ - [[Installing and Starting Jack]]
* __Windows__ - Install SuperCollider manually (and follow the instructions for the external server that appear later on)
* __OS X__ - No extra steps necessary

### Creating a Project Directory & Fetching Dependencies

Here we detail options for using [leiningen](http://github.com/technomancy/leiningen)to help you manage and fetch Overtone's dependencies.

__Note - if you wish to specify Clojure in your dependencies ensure that it is at least version `1.3.0`__

-------------
#### Leiningen
Create a new project

```sh
$ lein new tutorial
```

Add Overtone to the dependency list in `tutorial/project.clj`:

```clj
(defproject tutorial "1.0"
  :dependencies [ [org.clojure/clojure "1.3.0"]
                  [overtone "0.7.1"] ])
```

Pull in the dependencies

```sh
$ cd tutorial
$ lein deps
```

Dependencies will be obtained automatically on the first build.

### Downloading SuperCollider (for external servers only)

Head over to the [SuperCollider download site](http://supercollider.sourceforge.net/downloads/) and download and install the version appropriate for your operating system.

### What next?

Familiarise yourself with the process of [[Starting a REPL]] and [[Connecting scsynth]] then head over to [[Getting Started]] to learn how to make some crazy sounds. If you want to run the latest and greatest development version of Overtone have look at [[Overtone on the Edge!]]
