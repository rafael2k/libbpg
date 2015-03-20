Build dependencies on Debian/Ubuntu are:
build-essential libpng16-dev libjpeg8-dev libsdl1.2-dev libsdl-image1.2-dev libx265-dev

You might have to build libpng16-dev and libx265-dev manually:
http://download.sourceforge.net/libpng/libpng-1.6.16.tar.xz
https://bitbucket.org/multicoreware/x265

To build the javascript decoders from source, you'll need emscripten (including clang) and nodejs:
`sudo apt-get install emscripten nodejs`

On Debian and Ubuntu (maybe on other systems too) either clang or emscripten might be incompatible.
In this case you can build a portable version of emscripten and clang:
```
sudo apt-get build-essential cmake python2.7 nodejs default-jre git
wget https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz
tar xvf emsdk-portable.tar.gz
cd emsdk_portable
./emsdk update
./emsdk install latest
./emsdk activate latest
```

Run `source ./emsdk_env.sh` before you start building libbpg.
And you should set `NODE_JS = 'nodejs'` in ~/.emscripten.

