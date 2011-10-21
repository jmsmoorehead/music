For those intrepid live-coding adventurers that are looking for that more immersive connection with your Overtone musical processes TouchOSC is an excellent tool to play with:

http://hexler.net/software/touchosc
http://hexler.net/software/touchosc-android

It's super easy to use it to control and trigger synths and other functionality you might build on top of Overtone and it's an excellent way to start playing around and exploring with parameters whilst you're just starting and finding your way around the vast library of ugens.

Let's look how we can get TouchOSC talking to Overtone.

### Start an OSC Server

First up, we need to start an OSC server from within Overtone. This will listen on a specific port for incoming OSC messages sent from external OSC clients such as TouchOSC. Overtone embeds the [osc-clj](http://github.com/overtone/osc-clj) library which allows us to do exactly this. (Check out the [osc-clj README](https://github.com/overtone/osc-clj/blob/master/README.md) for more information about osc-clj's functionality).

Starting a server is simple, we just need to think of a port number. Let's go with 44100 because it fits with our musical context:

    (def server (osc-server 44100 "osc-clj"))

The string `"osc-clj"` is optional, but allows us to specify an identifier for our server which we can then refer to if we use zero-conf to help us connect a TouchOSC client. If you think you're going to be on a network with a lot of other people doing exactly this - then be sure to choose a unique name :-)

### Find or broadcast your network address

You'll either need to know the network address of the machine running Overtone, or you should use the zero-conf facility to broadcast this for you. So, find your network address or issue the following command:

    (zero-conf-on)

### Connect TouchOSC

Fire up TouchOSC, and head to the preference pane. It should look something like this:

![TouchOSC Preference Pane](http://cloud.github.com/downloads/overtone/overtone/touchosc-prefs.png)

Head to the OSC Connections sub-pane (at the top of the Connections options in the above image). This should looks as follows (assuming you chose to turn zero-conf on):

![TouchOSC OSC Connection Preference Pane](http://cloud.github.com/downloads/overtone/overtone/touchosc-osc-prefs.png)

Ensure sure that the OSC Connection is enabled (if necessary, set the on/off slider in the top right to on). Now, notice how our server we named `osc-clj` is listed as one of the "Found Hosts". All we need to do is tap that and TouchOSC will auto-configure our settings. Head back to Overtone and enter `(zero-conf-off)` to stop broadcasting your connection settings. 

If you didn't opt to use zero-conf, simply manually enter the port address of the server `44100` and your local IP address in this pane.

### Test Your Connection

Now, so far so good - but how do we know that the configuration worked? Let's register a listener on the OSC server which will run a function for each incoming OSC message and get it to just print out the contents of each message. This is pretty simple:

    (osc-listen server (fn [msg] (println msg)) :debug)

Now, over in TouchOSC, choose a layout and navigate to it (by pressing "Done" in the main preference pane). You should see something like this:

![Example TouchOSC Interface](http://cloud.github.com/downloads/overtone/overtone/touchosc-interface.png)

Now hammer on buttons/sliders etc. and be delighted with a streaming set of debug messages within Overtone. Note, you may have to be tailing a log file to view this output depending on your setup as it will be printed from a non-REPL thread. In cake you should `tail -f PROJECT-ROOT/.cake/cake.log`.



