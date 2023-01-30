# Carnets
Carnets is a stand-alone Jupyter notebook server and client. Edit your notebooks on the go, even where there is no network.

# To install without building: 

Carnets is now available on the [AppStore](https://holzschu.github.io/Carnets_Jupyter/). 

For the latest version, use the [TestFlight](https://testflight.apple.com/join/yevwlUs1) link. This version has more features, but also more bugs.

If the link doesn't work, you can also send an [e-mail](mailto:carnets_jupyter@icloud.com) to receive a TestFlight invitation. 

# To build it yourself: 
- clone the git repository
- type `./get_frameworks.sh`
- compile the Python frameworks: 
    - change into the `cpython` directory: `cd cpython`
    - `sh ./downloadAndCompile.sh` (this will download auxiliary frameworks, then compile cpython for OSX, iOS and Simulator)
    - the compile script may need some tuning depending on the version of XCode installed on your machine. 
- open Xcode, change the developer key, compile and install.

# Known issues / things to do:

- See [Project summary](https://github.com/holzschu/Carnets/projects/1)
- We are leaking 8-9 file descriptors for each kernel launch, and one thread. Trying to addres either of these results in *more* file descriptors being leaked.
- Ability to open notebooks in other applications (Safari, Juno...)

# Recently fixed bugs:

- Keyboard extension for iPads
- Opening files in iCloud
- Back/Forward buttons
- Save notebooks when app becomes inactive / background.
- Save last open notebook and restore when the app reopens.
- Better user interface for startup screen / ability to open notebooks everywhere, in place.
- You can't have more than 5 kernels running simultaneously. 
- Related: silently terminate oldest kernel when we approach the maximum number of kernels.
- "Terminals" don't work. Todo: Remove the option from the menus.
- Fixed: Starting the 10th or so kernel fails with `zmq.error.ZMQError: Too many open files`
- "new file", "new notebook", "copy notebook" now open a new window (instead of opening a blank window).
- Issue #3: "Kernel / restart and run all" does not work (kernel shudown followed by kernel restart does). Fixed with 9e3faa7
- Issue #2: `pip install` does not work (the package is unavailable, but the install process appears to have worked). Fixed with ee4cdc7

# To install new packages:

If it's a pure python package, you can install it yourself:

```python
%pip install packageName
```
and remove it if it doesn't work: 
```python
%pip uninstall -y packageName
```
(you need the "-y" flag because there is no interaction) 

Otherwise, open an [issue](https://github.com/holzschu/carnets/issues) and I'll add it to the default packages. 
