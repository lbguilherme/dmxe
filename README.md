# Docker MXE

This is an experimental Docker-based version of [MXE](http://mxe.cc/).

MXE is a nice cross compiling environment with many free libraries. See their site for more.

# What do I need?

The **only** dependency here is Docker itself, everything else will automatically happen inside the Docker container.

# Getting started

1. Clone this repo or download a tarball:
	```sh
	git clone https://github.com/lbguilherme/dmxe
	cd dmxe
	```

2. Prepare the MXE image. This will fetch the lastest Debian image and install all dependencies. Then it will clone the mxe repo inside it.
	```sh
	./dmxe prepare
	```

3. Make the libraries you need. This will launch the container and invoke `make` there with whatever you pass here:
	```sh
	./dmxe make gcc
	```
    
4. Create your first code to compile with MXE. For example:
	```c
	// main.c
	#include <windows.h>
	
	int main() {
		MessageBoxA(0, "Hello World from Docker MXE!", "MXE", MB_OK);
		return 0;
	}
	```

5. Run the image you have just built:
	```sh
	./dmxe run
	```

	You will be presented with a shell where you can access your current directory:
	```sh
	mxe@default:~$
	```

6. Simply compile your file and exit. `i686-w64-mingw32.static-gcc` here is the cross compiler for the default target:
	```sh
	mxe@default:~$ i686-w64-mingw32.static-gcc main.c -o main.exe
	mxe@default:~$ exit
	```
    
7. Take a look on the file you have produced:
	```sh
	file main.exe
	# main.exe: PE32 executable (console) Intel 80386, for MS Windows
	```

8. Run it! [Wine](https://www.winehq.org/) is your friend.
	```sh
	wine main.exe
	```

	![screenshot of main.exe](http://lbguilherme.com/screenshot/e97fbc3201d9829a500bd8880af6f513.jpg)
