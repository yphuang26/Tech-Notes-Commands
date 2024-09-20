
Simply use pre-defined `$OSTYPE` variable.
### if ... else
---
```shell
if [[ "$OSTYPE" == "linux-gnu"* ]]; then
	# Linux
elif [[ "$OSTYPE" == "darwin"* ]]; then
	# MaxOS
elif [[ "$OSTYPE" == "cygwin" ]]; then
	# POSIX compatibility layer and Linux environment emulation for Windows
elif [[ "$OSTYPE" == "msys" ]]; then
	# Lightweight shell and GNU utilities compiled for Windows (part of MinGW)
elif [[ "$OSTYPE" == "win32" ]]; then
	# Win32
else
	# Unknown
fi
```
### case
---
```shell
case "$OSTYPE" in
  solaris*) echo "SOLARIS" ;;
  darwin*)  echo "OSX" ;; 
  linux*)   echo "LINUX" ;;
  bsd*)     echo "BSD" ;;
  msys*)    echo "WINDOWS" ;;
  cygwin*)  echo "ALSO WINDOWS" ;;
  *)        echo "unknown: $OSTYPE" ;;
esac
```
