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

