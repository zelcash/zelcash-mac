# Zelcash Builder for Apple Platform

![Screenshot](https://github.com/kozyilmaz/zcash-apple/raw/master/docs/zcash-apple.png "Zelcash on Mac OS")

**This project requires Xcode 9 and a Mac running macOS 10.12.6 or later.**  
This repository builds standalone Zelcash binaries for macOS platform without installing brew.  
All build tools (`autoconf, automake, libtool, pkgconfig, cmake, install and readlink`) and `Zelcash` are compiled from scratch.  


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

In case of an error please run the following command for debug info
```shell
$ PRINT_DEBUG=y make all
```

After successful build Zelcash binaries will be installed to `out` directory under project root  
You can then copy binary directory anywhere you like there are no dependencies to the build tree anymore  
```shell
bash-3.2$ ls -lrt out/usr/local/bin
total 32136
-rwxr-xr-x@ 1 loki  staff       483 Feb 25 21:19 zelcash-init
-rw-r--r--@ 1 loki  staff      1766 Feb 25 21:19 zelcash-commands.txt
-rwxr-xr-x@ 1 loki  staff  13369544 Feb 25 21:39 zelcashd
-rwxr-xr-x@ 1 loki  staff   1814860 Feb 25 21:39 zelcash-tx
-rwxr-xr-x@ 1 loki  staff      4761 Feb 25 21:39 zcash-fetch-params
-rwxr-xr-x@ 1 loki  staff   1238732 Feb 25 21:39 zelcash-cli
-rw-r--r--@ 1 loki  staff        54 Feb 25 21:39 version.txt
bash-3.2$ otool -L out/usr/local/bin/zelcashd
out/usr/local/bin/zelcashd:
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
bash-3.2$ otool -L out/usr/local/bin/zelcash-cli 
out/usr/local/bin/zelcash-cli:
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
bash-3.2$ otool -L out/usr/local/bin/zelcash-tx
out/usr/local/bin/zelcash-tx:
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
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

You can just run `Zelcash` by launching the daemon afterwards. After blockchain is sync'd, you can use the sample commands provided in [zelcash-commands.txt](zelcash/files/zelcash-commands.txt)  

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
/Users/USERNAME/Library/Application Support/ZcashParams/README

Retrieving: https://z.cash/downloads/sprout-proving.key
######################################################################## 100.0%
/Users/USERNAME/Library/Application Support/ZcashParams/sprout-proving.key.dl: OK
/Users/USERNAME/Library/Application Support/ZcashParams/sprout-proving.key.dl -> /Users/USERNAME/Library/Application Support/ZcashParams/sprout-proving.key
Retrieving: https://z.cash/downloads/sprout-verifying.key
######################################################################## 100.0%
/Users/USERNAME/Library/Application Support/ZcashParams/sprout-verifying.key.dl: OK
/Users/USERNAME/Library/Application Support/ZcashParams/sprout-verifying.key.dl -> /Users/USERNAME/Library/Application Support/ZcashParams/sprout-verifying.key
bash-3.2$ 
bash-3.2$ cat zelcash-init 
#!/bin/bash

# excerpted from zclassic/zutil/init-mac.sh

if [ ! -f "$HOME/Library/Application Support/zelcash/zelcash.conf" ]; then
    echo "Creating zelcash.conf"
    mkdir -p "$HOME/Library/Application Support/zelcash/"
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

## Thanks
Developers of `Zcash`  
Developers of `ZClassic` for MacOS patches
Developers of `Zelcash Foundation`

## Donations
If you feel this project is useful to you. Feel free to donate.

    BTC address: 1GmXRm5sEATy3Kz1hCxS1dwfXuCPkevsa
    ZEL address: 


### Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

