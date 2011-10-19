At this point we assume that you have [[installed Overtone|Installing Overtone]] and [[started a REPL|Starting a REPL]]. You should be in the position where you see the following on your terminal:

    user=>

Clojure is sitting there waiting for your next command, silent and obediently. What shall we ask of it? Well, if we wish it to make our speakers sing out the glorious swelling flush of powerful angelic wings rushing by, we need to load up an Overtone environment and connect to an scsynth server. So, let's get cracking. However, before we get started, we need a quick chat about servers.

### The Difference between External & Internal Servers

Overtone supports both internal and external instances the SuperCollider server (fondly referred to as scsynth - for SuperCollider Synth). The internal server is good for quick setup (there are no external dependencies to install and allows fast access to server buffers for transferring sound data and using the scopes). The external server requires a separate installation of SuperCollider itself but is more robust in that crashes in the server (through malformed synth designs etc.) don't also crash the JVM (which is the case for the internal server). It is also possible to connect multiple separate clients to an already running external scsynth instance.

Note - the internal server is not currently supported for all architecture/operating system combinations. However, the external server should work everywhere.

Let's summarise that:

* Internal Server
  - Good - Using the scope to visualise audio and buffers. Fast retrieval of audio buffers. Super simple to use.
  - Bad  - Crashes whole JVM when scsynth crashes, doesn't work everywhere and doesn't allow for multiple clients to connect to the same server (although you can coordinate external systems through Overtone itself)
* External Server
  - Good - More robust setup. Allows for multiple clients to be connected to the same server.
  - Bad  - No scope or fast audio buffer retrieval (although you still can access buffer data much more slowly)

OK, let's discuss connecting to internal and external servers separately.

### Connecting to an Internal Server

This is super easy. We simply issue the following statement to our Clojure REPL:

    user=>(use 'overtone.live)

Clojure will then diligently fire up an internal server process and connect to it for us. When the prompt returns, we're ready to go.

### Connecting to an External Server

In order to connect to an external server you need to manually install SuperCollider. Head here: http://supercollider.sourceforge.net/ and install a version for your architecture. If you're running Linux, make sure that the `scsynth` executable is in your `PATH`.

Before you connect you need to choose whether you want to boot or connect.

##Connect to a currently running server

* make sure your server is running. (If you're using the standard SuperCollider distribution this will mean booting the 'localhost' server). 
* find out which port the server is listening on (this is typically `57110` for the SuperCollider localhost server)
* use `overtone.core` either directly or in your `ns` declaration
* call `(connect-external-server 57110)` (replacing the port with the specific port you wish to use.)
* If the server is on a different machine use `(connect-external-server "192.168.1.23" 57110)` substituting the appropriate hostname and port number

##Explicitly boot a server from within Overtone

* use `overtone.core` either directly or in your `ns` declaration
* call `(boot-external-server)`

Now you can continue to use Overtone as usual - define synths, trigger them, have fun!