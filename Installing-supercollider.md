NOTE: Please help keep this page up to date!  Feel free to update these instructions if you run into problems on a specific platform or with a certain install method.

### Checkout, build and install the latest Supercollider:

`git clone git://supercollider.git.sourceforge.net/gitroot/supercollider/supercollider`
`cd supercollider`
`git submodule init`
`git submodule update`
`mkdir build`
`cd build`
`cmake ..`

If you don't have QT or don't want the QT gui you can turn it off like this: 
`cmake -DSC_QT=OFF ..`

Now compile and install:
`make`
`sudo make install`

### Checkout, build and install the latest SC3-Plugins:

`cd ..`
`git clone git://sc3-plugins.git.sourceforge.net/gitroot/sc3-plugins/sc3-plugins`
`cd sc3-plugins`
`mkdir cmake_build`
`cd cmake_build`

Now you need to point cmake to your installed SuperCollider.  On Linux the standard install from source goes to /usr/local/include/SuperCollider/.

`cmake -DSC_PATH=/path/to/include/supercollider/ ..`
`make`
`sudo make install`

### Run supercollider

Listening on UDP port 2345:

`/usr/local/bin/scsynth -u 2345`

