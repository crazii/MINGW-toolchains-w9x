# MINGW-toolchains-w9x
MINGW toolchains for building Win9x target

Build scripts copied from https://github.com/msys2/MINGW-packages and added with '-march=pentium3' flags to support legacy CPUs.

# HOWTO BUILD
Edit /etc/makepkg_mingw.conf in mingw or "${C:\Msys64}\etc\makepkg_mingw.conf" on your host pc,
to change 
```
CFLAGS="-march=pentium4 -mtune=generic -O2 -pipe -Wp,-D_FORTIFY_SOURCE=2 -fstack-protector-strong"
CXXFLAGS="-march=pentium4 -mtune=generic -O2 -pipe"
```
into
```
CFLAGS="-march=pentium3 -mtune=generic -O2 -pipe -Wp,-D_FORTIFY_SOURCE=2 -fstack-protector-strong"
CXXFLAGS="-march=pentium3 -mtune=generic -O2 -pipe"
```
in ```elif [[ "$MSYSTEM" == "MINGW32" ]]; then``` branch.

or chanage to -march=pentium for win95/NT targets.

In mingw32/64,
run
 ```
cd ${package-name}
MINGW_ARCH=mingw32 makepkg-mingw -sLf
pacman -U ${package-name}*.pkg.tar.zst
```
This will overwrite your local install packages, backup them if needed.
