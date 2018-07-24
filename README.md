# box-package-manager
A simple package manager for [Shoebox Linux](https://github.com/antoniusmisfit/shoebox-linux).
## Basic usage
```
box install path/to/package.box
box remove PackageName
```
## Extending Box Package Manager
The Box package manager is easily extensible.In fact, the main "box" script doesn't do anything other than pass execution to a "box-$command" executable on the system $PATH. Here is a trivial example of adding a "convert" command which copies a Box package into a plain old .tar.gz file:
```
cat > /usr/local/bin/box-convert << EOF
#!/bin/sh

cp \$1 $(basename \$1 .box).tar.gz
chmod +x /usr/local/bin/box-convert
EOF
```
## Packaging your own software with Box
A .box package is actually nothing more than a gzipped tar file containing the software to be installed, a manifest file providing important data to the developer/user and Box itself, and two scripts to be run during installation and removal of the package(pkginst and pkgrm, respectively).

The manifest file follows this simple format:
```
PackageName: Box
Version: 0.1
Maintainer: Tony Agudo <antoniusmisfit@gmail.com>
Desc: A simple package manager for Shoebox Linux.
Deps: Busybox, Tar

Box is a simple and easily extensible package manager for Shoebox Linux and similar Linux distributions.
```
The installation and removal scripts are usually shell scripts, but depending on the software being packaged, they could be written in any language as long as they are recognized as executable by the system Box is installed on.

The filesystem layout of a simple Box package is as follows:
```
+-/
  |-MANIFEST
  |-pkginst
  |-pkgrm
  +-usr/
    +-local/
      +-bin/
        |-box
        |-box-install
        |-box-remove
        |-box-build
```
e
To create the final .box package after setting up the proper file structure, you may directly use the tar command or a nice GUI frontend like xarchiver to create a .tar.gz file, then rename the extension to .box.
