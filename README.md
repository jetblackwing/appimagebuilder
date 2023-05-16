# appimagebuilder
A minimal automated AppImage Builder tool for Linux, inspired from AppImageKit



Don't even try to run. This is just an initial commit, which means it is yet to test on devices.

If you still want to try anyway, go ahead.
Basic Setup as of now:
## appimagebuilder usage

`appimagebuilder or aib` is used to generate an AppImage from an existing `AppDir`. A precompiled version can be found on [GitHub Releases](https://github.com/AppImage/AppImageKit/releases).


```


Usage:
  aib [OPTION...] SOURCE [DESTINATION] - Generate, extract, and inspect AppImages

Help Options:
  -h, --help                  Show help options

Application Options:
  -l, --list                  List files in SOURCE AppImage
  -u, --updateinformation     Embed update information STRING; if zsyncmake is installed, generate zsync file
  -g, --guess                 Guess update information based on Travis CI or GitLab environment variables
  --bintray-user              Bintray user name
  --bintray-repo              Bintray repository
  --version                   Show version number
  -v, --verbose               Produce verbose output
  -s, --sign                  Sign with gpg[2]
  --comp                      Squashfs compression
  -n, --no-appstream          Do not check AppStream metadata
  --exclude-file              Uses given file as exclude file for mksquashfs, in addition to .appimageignore.
  --runtime-file              Runtime file to use
  --sign-key                  Key ID to use for gpg[2] signatures
  --sign-args                 Extra arguments to use when signing with gpg[2]
```

If you want to generate an AppImage manually, you can:

```
mksquashfs Your.AppDir Your.squashfs -root-owned -noappend
cat runtime >> Your.AppImage
cat Your.squashfs >> Your.AppImage
chmod a+x Your.AppImage
```


## Building

__NOTE:__ This is still testing.

Our build system is based on Docker. To build your own binaries, please install Docker first. Then, follow the following steps:

```
git clone --single-branch --recursive https://github.com/AppImage/AppImageKit
cd AppImageKit/
bash ci/build.sh
```

This will create the binaries in a directory called `out/`.

Please note: It is not recommended nor supported to build AppImageKit on any newer build system than the oldest still-supported versions of major distributions for reasons outlined [here](https://github.com/AppImage/AppImageKit/wiki/Creating-AppImages#creating-appimages-that-are-compatible-with-many-systems). Currently we are targeting CentOS 6.x and Ubuntu 14.04 as build systems and we are not interested to build AppImageKit on newer versions anytime soon. Binaries built on those systems will run just fine on newer (later) target systems (distributions).
