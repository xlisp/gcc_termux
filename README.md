
## For mcp 2025 update, test pass

```
pkg install vim git openssh python

pkg install  rust cmake clang  fftw libzmq freetype libpng pkg-config libcrypt

pip install "mcp[cli]" 


pkg install  matplotlib


pip install  pandas

pip install jupyter

```

---

From now on im using apt for updates
add 

```bash
deb [trusted=yes] https://its-pointless.github.io/files/  termux extras
```

to sources.list or add a file with .list suffix in ` $PREFIX/etc/apt/sources.list.d/ `
gpg key is https://its-pointless.github.io/pointless.gpg
if not installed install gnupg

```bash
echo "deb [trusted=yes] https://its-pointless.github.io/files/  termux extras" >> $PREFIX/etc/apt/sources.list.d/sources.list

apt-get install gnupg
wget https://its-pointless.github.io/pointless.gpg
apt-key add pointless.gpg ## will add the key to apt
apt-get update

## 
wget https://its-pointless.github.io/setup-pointless-repo.sh
bash setup-pointless-repo.sh

```

or use https://its-pointless.github.io/setup-pointless-repo.sh

use the commands setupclang setupclang and setupgcc-7 to switch compilers
nothing complex just moving symlinks around
30/03/2018

julia is compiling on all archs but must be done on device. see my android-termux branch 
of julia. Also added an arm build for testing...



20/03/2018

TESTING openblas for x86_64 atom....


7/02/2018

added povray because ... i don't know.


10/01/2018

updated rustc and rustc-nightlies
fixed issues on x86_64 gcc
added racket for arm and i686


5/01/2018
changed gcc-7 sources to linaro ... because why not? going to add source so 
everyone can compile and won't rely on me providing binaries... at all. 

added gnatmake for arm ( other archs are not likely to come since it requires
a sigtramp implentation that is absent on android)

added racket ... likely buggy for arm and i686. not working yet on 64 bit archs

also adding libboostpython libs which is a pull request for termux/termux-packages 

23/12/2017
updated ecl arm and julia for x86_64. both should now work again

20/12/2017

updated cargo for all but i686
updated rustc-nightly for and added for i686. not on x86_64...
if i have time i will work on it. Ecl should now compile maxima
technically there aren't any "major" dependencies missing for sagemath 
would have to built on device though...


13/12/2017
added ecl rustc nightly for arm and aarch64. 
added the cross_config stuff for ecl as well.

28/11/2017
added libgomp for gcc-7 in 7.2.0 and ndk 4.9.x flavours
Thanks to @arietal libcairo now works in R. 
also added julia lang for i686 x86_64. 
I have no idea how long or if ever arm and aarch64 will take. 

19/11/2017
r-cran package 3.4.2-1 uploading, should be working again... enabled openmp because i can.
pforth 32 bit fix upload for testing.
should get  updated scipy and numpy at some point hopefully soon

11/11/2017 
rustc now working for x86_64 and i686. The bug with cargo on arm is also fixed.
As libgit2 needed to be compiled with -no-integrated-as the fix is statically linked.



08/10/2017
added python 2 versions numpy and scipy


01/10/2017
guile 2.0 and 2.2 added
i686 version for 2.0 has threads disabled due to crashing half the time.
2.2 has no such issue as far as I can tell but the build process for 2.2 builds
needs some work before a pull request to main repo.


12/09/2017
rustc is broken if you upgraded libllvm to 5.0 
to rememdy that install newly added package libllvm-4so should be working from there



08/09/2017

added fixedshe package and command executing it will start a new shell with
LD_PRELOAD=$PREFIX/lib/libandroid-fixshebang.so $shell
this will cause commands /bin/sh and /usr/bin/env to be redirected making shebangs with those 
commands work. to change default shell to do this the command fixedshe chsh will work as chsh does.

Doing this will enable  R and Octave library installs to work correctly first time much more often
things like fixedshe octave also work


27/08/2017

added openldap f0r testing need feedback 

updated gcc to 7.2 

added more stuff to x86_64 ans i686



08/08/2017
adding i686 and x86_64  stuff 
cargo and rusttc 
octave and R
etc
also some experimental nodejs 8.2.1 builds ...



29/07/2017

to get cargo for arm working add this to ~/.gitconfig 

[url "git://github.com/rust-lang/crates.io-index"]
        insteadOf = https://github.com/rust-lang/crates.io-index


25/07/2017
octave is fixed and back up on repo as well as gmic arm.

24/07/2017
octave isn't working right now ... 

23/07/2017
a working gmic binoary for arm required some magic getting it...


22/07/2017

gmic is not working for arm and it appears to be stubborn about it.
sorry about that. 


17/07/2017

Got almost everything working with the transision to libc++_shared. Updating the apt
repo shortyly there are a few packages there that are not not mentioned here... 







27/05/2017
added rustc and cargo for arm and aarch64 from @vishalbiswas
a bit buggy for now 


24/05/2017

Added quantlib. Will be adding R stuff shortly. Mpd-ext is also in repo extended for modpluglib and
libgme. So game emulation music plays. Haven't tested that yet should work.  



just added imgflo ... i haven't tested it if someoen wants to inform me how its screwed 
i would be thankful.
updated now with termux-packages pull requests as well

electrum egg added ...
updates
added boost ledger r-cran 
the mpv-ext is just mpv with caca enabled and alpine has been updated.


Octave seems to be working fairly well...
report bugs???
Its less annoying to compile than R so i might fix things that are really broken. 
The scripts to compile fortran stuff needs a bit of work to be more user friendly 
and less of a hack. 

termux gcc resurrected purely because scipy needs it. 
Don't annoy fornwall if you find a bug since its 
entirely unsupported. 
This is a compiler of last resort hecause you 
need to compile fortran or something needs gcc and
only gcc.


For scipy to work you need blaslib(openblas, reference blas +lapack or atlas) libgfortran
numpy and scipy.

```bash

apt install openblas
apt install  libgfortran5
apt install libgomp-10

apt install scipy && apt install python2-scipy # 不用自己编译 LDFLAGS=" -lm -lcompiler_rt" pip2.7 install scipy

apt install clang  fftw libzmq freetype libpng pkg-config libcrypt

LDFLAGS="-lm -lcompiler_rt" pip install jupyter
LDFLAGS="-lm -lcompiler_rt" pip install  matplotlib


```

If you want to do this yourself its not hard.
https://github.com/xianyi/OpenBLAS/wiki/How-to-build-OpenBLAS-for-Android
I compiled arm and arm64 tool chain for linux x86_64 (the .tar.bz2 file)
so you can extract over the android ndk tool chain for ndk-13 and when termux creates tool chain it should
pull stuff in. 
https://github.com/xianyi/OpenBLAS/wiki/How-to-build-OpenBLAS-for-Android

The default makefile for openblas uses hardfp and termux uses softfp so it won't work
on termux. Don't use it on arm use either lapack or atlas. Atlas will likely be faster
than lapack. 

LDFLAGS when compiling scipy and numpy for distribution is important. You can compile on android 6.0 and it might not 
work on 5.1 because the linker is different. 

#### julia install 

* https://askubuntu.com/questions/141370/how-to-fix-a-broken-package-when-apt-get-install-f-does-not-work

```bash

## 处理 ` apt install libgfortran libgfortran5` 安装失败的问题
$ dpkg -i --force-overwrite /data/data/com.termux/files/usr/var/cache/apt/archives/libgfortran5_8.1.0_aarch64.deb

➜  ~ julia
               _
   _       _ _(_)_     |  A fresh approach to technical computing
  (_)     | (_) (_)    |  Documentation: https://docs.julialang.org
   _ _   _| |_  __ _   |  Type "?help" for help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 0.7.0-DEV.5015 (2018-05-05 13:38 UTC)
 _/ |\__'_|_|_|\__'_|  |  android-termux/3bd8503c61* (fork: 8 commits, 3 days)
|__/                   |  aarch64--linux-android

julia>

```

