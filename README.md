Build scripts for ffmpeg on iPhone SDK 3.0 (and iPhone Simulator SDK).

## Scripts 

- `build-[arch]`: Build scripts for each arch; Run these first and then `combine-ffmpeg-libs`
- `combine-libs`: Creates universal binaries; Runs lipo -create on each of the ffmpeg static libs

- `build-x264-[arch]`: x264 build scripts for each arch; Run these before normal build script to include x264 support
- `combine-x264-libs`: Creates universal binaries; Runs lipo -create on each of the x264 static libs

- `build-xvid-[arch]`: xvid build scripts for each arch; Run these before normal build script to include xvid support


## Revision

The current ffmpeg trunk doesn't build with arm, so had to go back to r22404 in order to build arm targets. The i386 build does work on trunk (r22610) when I tried last.

The changes that broke compilation are from:
http://git.ffmpeg.org/?p=ffmpeg;a=commitdiff;h=af29d08a05d35c3b74e48d5f6c5cd56f1770eeca

The gas-preprocessor breaks because of nested macros in arm/asm.S; I believe there are other issues as well though.

## Background

For background, follow this thread:
http://lists.mplayerhq.hu/pipermail/ffmpeg-devel/2009-October/076618.html

To make lipo'able libraries, you need to use gcc-4.2 with extra cflags instead of the specific arm-apple-darwin10-gcc-4.2.1 compiler.

The armv6 arch doesn't seem to be working properly so you can force building via armv7 on your 3GS until we figure that out.

## X264

For x264 support in ffmpeg, run those build scripts first, and the ffmpeg build scripts will include it.

## Gas preprocessor

Uses a modified gas preprocessor via http://github.com/yuvi/gas-preprocessor/

