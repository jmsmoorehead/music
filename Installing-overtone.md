Installing Overtone can be trivia or complex depending on your previous experience with Clojure projects, desire to use an external SuperCollider server and target OS. Here we'll walk you through all the steps assuming you have little or no prior Clojure knowledge.

Essentially, installation consists of the following steps:

* Perform any necessary OS-specific setup
* Create a new directory for your audio project
* Download the appropriate dependencies
* Download and install SuperCollider (if you wish to use an external server)
* Start a REPL
* Boot or connect to a SuperCollider server
* Start hacking music!

### OS-specific setup

#### Linux
* [[Installing and Starting Jack]]

#### Windows
Watch this space

#### OS X
No extra steps necessary


### Creating a Project Directory & Fetching Dependencies

__Note - if you wish to specify Clojure in your dependencies ensure that it is at least version `1.3.0`__

#### Cake
If you wish to use [cake](http://clojure-cake.org/):

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

#### Leiningen
If you wish to use [leiningen](http://github.com/technomancy/leiningen)

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

#### Maven
If you wish to use [Maven](http://maven.apache.org/):

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
