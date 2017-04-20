# Little Endian zpugcc

This is a version of the ZPU toolchain for a little endian GPU.

## Background

The ZPU (https://github.com/zylin/zpu) is a tiny 32 bit CPU designed for FPGAs. It is normally big endian, which makes sense for a hardware implementation. For software emulation on a little endian machine, though, the big endian architecture imposes a performance penalty. So this toolchain is adapted for a little endian variant of the ZPU, for example emulated on the little endian Parallax Propeller (https://github.com/totalspectrum/zog).

## Caveats

The tools have all been ported to little endian, but the runtime exception handlers have not. In particular, emulation of loadb/loadh/storeb/storeh will not work correctly. That's not a problem if those instructions are implemented in hardware (or emulated directly). If you're trying to implement a little endian version of the ZPU in hardware make sure you either implement those instructions in hardware or else fix the emulation code.

## License

The various subdirectories have appropriate COPYING files in them. Generally most of the tools are under the GPL, whereas the runtime library is under the more permissive newlib license.

The changes I had to make to port the toolchain to little endian mode are in the file "little_endian.patch". You can revert those to get back the original big endian ZPU toolchain.

# Original Readme for zpugcc

This repository contain the gcc, which is adapted for https://github.com/zylin/zpu CPU,
the worlds smallest 32 bit CPU with GCC toolchain.

# ZPU toolchain source code
The ZPU toolchain is too big to be hosted together with the HDL and the idea is that most HDL or normal users would not want to download and build their own toolchain.

# ZPU build instructions to build unstable on linux (same for CygWin32)

    git clone https://github.com/zylin/zpugcc.git
    cd toolchain/toolchain
    sh fixperm.sh
    . env.sh
    sh build.sh
    tar -cjvf zpugcclinux_unstable.tar.bz2 install 

Build a different version

    git log => shows log entries
    git checkout 322875263beccb1d75936bd1dd9150c1647dc9c0 => checkout a version
    Note that build.sh is only present in the later versions, but that it should work fine for those versions in git where it is absent. 

# Cygwin build problems
If you are having problems building with Cygwin, try erasing the *entire* c:\cygwin folder and try again. 
