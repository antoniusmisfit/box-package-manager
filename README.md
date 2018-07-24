# box-package-manager
A simple package manager for Shoebox Linux.
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
