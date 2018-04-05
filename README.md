# Yet Another Zelcash Builder for Apple Platform

![Screenshot](https://github.com/kozyilmaz/zelcash-apple/raw/master/docs/zelcash-apple.png "Zelcash on Mac OS")

This repository builds standalone Zelcash binaries for macOS platform without installing brew.  
No additional dependency required except Xcode (https://developer.apple.com/xcode).  
All build tools (`autoconf, automake, libtool, pkgconfig, cmake, install and readlink`) and `Zelcash` are compiled from scratch (finally with `clang`).  


### Build instructions
```shell
# run once to install Xcode CLI tools
$ xcode-select --install
# clone and build Zelcash on macOS
$ git clone https://github.com/Lumiboy/zelcash-mac.git
$ cd zelcash-mac
$ source environment
$ make
```

After successful build Zelcash binaries will be installed to `out` directory under project root  
You can then copy binary directory anywhere you like there are no dependencies to the build tree anymore  
```shell
bash-3.2$ ls -lrt out/usr/local/bin
total 31544
-rwxr-xr-x  1 loki  staff       483 Dec 16 15:56 zelcash-init
-rwxr-xr-x  1 loki  staff  13120252 Dec 20 01:06 zelcashd
-rwxr-xr-x  1 loki  staff   1772400 Dec 20 01:06 zelcash-tx
-rwxr-xr-x  1 loki  staff      4761 Dec 20 01:06 zcash-fetch-params
-rwxr-xr-x  1 loki  staff   1237116 Dec 20 01:06 zelcash-cli
bash-3.2$ otool -L out/usr/local/bin/zelcashd
out/usr/local/bin/zelcashd:
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 307.5.0)
bash-3.2$ otool -L out/usr/local/bin/zelcash-cli 
out/usr/local/bin/zelcash-cli:
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 307.5.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
bash-3.2$ otool -L out/usr/local/bin/zelcash-tx
out/usr/local/bin/zelcash-tx:
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 307.5.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
```

### Run instructions

When launching `Zelcash` on MacOS for the first time, certain initalization steps should be completed.  
Please run the commands below once for the first time  

```shell
$ cd out/usr/local/bin
$ ./zcash-fetch-params
$ ./zelcash-init
$ ./zelcashd
```

You can just run `Zelcash` by launching the daemon afterwards  

`$ ./zelcashd`  

Console output from the first run is below:
```shell
bash-3.2$ ./zcash-fetch-params
Zelcash - fetch-params.sh

This script will fetch the Zelcash zkSNARK parameters and verify their
integrity with sha256sum.

If they already exist locally, it will exit now and do nothing else.
The parameters are currently just under 911MB in size, so plan accordingly
for your bandwidth constraints. If the files are already present and
have the correct sha256sum, no networking is used.

Creating params directory. For details about this directory, see:
/Users/loki/Library/Application Support/ZcashParams/README

Retrieving: https://z.cash/downloads/sprout-proving.key
######################################################################## 100.0%
/Users/loki/Library/Application Support/ZcashParams/sprout-proving.key.dl: OK
/Users/loki/Library/Application Support/ZcashParams/sprout-proving.key.dl -> /Users/loki/Library/Application Support/ZcashParams/sprout-proving.key
Retrieving: https://z.cash/downloads/sprout-verifying.key
######################################################################## 100.0%
/Users/loki/Library/Application Support/ZcashParams/sprout-verifying.key.dl: OK
/Users/loki/Library/Application Support/ZcashParams/sprout-verifying.key.dl -> /Users/loki/Library/Application Support/ZcashParams/sprout-verifying.key
bash-3.2$ 
bash-3.2$ cat zelcash-init 
#!/bin/bash

# excerpted from zclassic/zutil/init-mac.sh

if [ ! -f "$HOME/Library/Application Support/zelcash/zelcash.conf" ]; then
    echo "Creating zelcash.conf"
    mkdir -p "$HOME/Library/Application Support/Zelcash/"
    echo "rpcuser=zelcashrpc" > ~/Library/Application\ Support/zelcash/zelcash.conf
    PASSWORD=$(cat /dev/urandom | env LC_CTYPE=C tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    echo "rpcpassword=$PASSWORD" >> "$HOME/Library/Application Support/zelcash/zelcash.conf"
    echo "Complete!"
fi
bash-3.2$ 
bash-3.2$ ./zelcash-init 
Creating zelcash.conf
Complete!
```

Vaklinov's [Desktop GUI Wallet](https://github.com/vaklinov/zelcash-swing-wallet-ui) also works, please follow build instructions for MacOS


## Thanks
Developers of `Zelcash`  
Developers of `ZClassic` for MacOS patches

## Donations
If you feel this project is useful to you. Feel free to donate.

    BTC address: 
    ZEL address: 


### Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

