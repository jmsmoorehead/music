When you include the `overtone.live` namespace, Overtone will automatically boot and connect to an internal SuperCollider server which is a very convenient way of working. However, in some cases you might wish to use a currently running (external) SuperCollider server. For example, you may wish to trigger and control synths defined in an SCLang session.

Connecting to external servers is simple:

* make sure your server is running. (If you're using the standard SuperCollider distribution this will mean booting the 'localhost' server). 
* find out which port the server is listening on (this is typically `57110` for the SuperCollider localhost server)
* use `overtone.core` either directly or in your `ns` declaration
* call `(connect 57110)` (replacing the port with the specific port you wish to use.

Now you can continue to use Overtone as usual - define synths, trigger them, have fun!
