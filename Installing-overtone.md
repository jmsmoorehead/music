Installing Overtone can be trivia or complex depending on your previous experience with Clojure projects, desire to use an external SuperCollider server and target OS. Here we'll walk you through all the steps assuming you have little or no prior Clojure knowledge.

Essentially, installation consists of the following steps:

* Perform any necessary OS-specific setup
* Create a new directory for your audio project
* Download the appropriate dependencies
* Download and install SuperCollider (if you wish to use an external server)

### OS-specific setup

* __Linux__ - [[Installing and Starting Jack]]
* __Windows__ - Watch this space
* __OS X__ - No extra steps necessary

### Creating a Project Directory & Fetching Dependencies

Here we detail options for using either [cake](http://clojure-cake.org/), [leiningen](http://github.com/technomancy/leiningen) or [Maven](http://maven.apache.org/) to help you manage and fetch Overtone's dependencies.
_Note - if you wish to specify Clojure in your dependencies ensure that it is at least version `1.3.0`_

#### Cake
Create a new project
```sh
$ cake new tutorial
```

Add Overtone to the dependency list in `tutorial/project.clj`:

```clj
(defproject tutorial "1.0"
  :dependencies [[overtone "0.5.0"]])
```

Pull in the dependencies
```sh
$ cd tutorial
$ cake deps
```

-------------
#### Leiningen
Create a new project
```sh
$ lein new tutorial
```

Add Overtone to the dependency list in `tutorial/project.clj`:

```clj
(defproject tutorial "1.0"
  :dependencies [[overtone "0.5.0"]])
```

Pull in the dependencies
```sh
$ cd tutorial
$ lein deps
```

-------------
#### Maven
Create a new directory for your project:

```sh
$ mkdir tutorial
```

Create a new file called `pom.xml` within the `tutorial` directory  with the following contents:
```xml
<dependency>
  <groupId>overtone</groupId>
  <artifactId>overtone</artifactId>
  <version>0.5.0</version>
</dependency>
```

Maven wizards - please complete this section.

### Downloading SuperCollider (for external servers only)

Head over to the [SuperCollider download site](http://supercollider.sourceforge.net/downloads/) and download and install the version appropriate for your operating system.

### What next?

Familiarise yourself with the process of [[Starting a REPL]] and [[Booting scsynth]] then head over to [[Getting Started]] to learn how to make some crazy sounds.
