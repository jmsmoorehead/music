At this point we assume that you have [[installed Overtone|Installing Overtone]] and [[started a REPL|Starting a REPL]]. You should be in the position where you see the following on your terminal:

    user=>

Clojure is sitting there waiting for your next command, silent and obediently. What shall we ask of it? Well, if we wish it to make our speakers sing out the glorious swelling flush of powerful angelic wings rushing by, we need to load up an Overtone environment and connect to an scsynth server. So, let's get cracking. However, before we get started, we need a quick chat about servers.

### The Difference between External & Internal Servers

Overtone supports both internal and external instances the SuperCollider server (fondly referred to as scsynth - for SuperCollider Synth). The internal server is good for quick setup (there are no external dependencies to install and allows fast access to server buffers for transferring sound data and using the scopes). The external server requires a separate installation of SuperCollider itself but is more robust in that crashes in the server (through malformed synth designs etc.) don't also crash the JVM (which is the case for the internal server). It is also possible to connect multiple separate clients to an already running external scsynth instance.

Note - the internal server is not currently supported for all architecture/operating system combinations. However, the external server should work everywhere.

Let's summarise that:

* Internal Server
  - Good - Using the scope to visualise audio and buffers. Fast retrieval of audio buffers.
  - Bad  - Crashes whole JVM when scsynth crashes, doesn't work everywhere.
* External Server
  - Good - More robust setup. Allows for multiple clients to be connected to the same server.
  - Bad  - No scope or fast audio buffer retrieval (although you still can access buffer data much more slowly)

OK, let's discuss connecting to internal and external servers separately.