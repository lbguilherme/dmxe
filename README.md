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

2. Build the MXE image. You can specify a target and a list of packages to include. This will take a while.
	```sh
	./dmxe build --target=i686-w64-mingw32.static gcc
	```
    
3. Create your first code to compile with MXE. For example:
	```c
	// main.c
	#include <windows.h>
	
	int main() {
		MessageBoxA(0, "Hello World from Docker MXE!", "MXE", MB_OK);
		return 0;
	}
	```

4. Run the image you have just built, with all options ready for you:
	```sh
	./dmxe run
	```

	You will be presented with a shell:
	```sh
	mxe@mxe:~$
	```

5. Simply compile your file and exit. `gcc` here is the cross compiler for the target you specified:
	```sh
	mxe@mxe:~$ gcc main.c -o main.exe
	mxe@mxe:~$ exit
	```
    
6. Take a look on the file you produced:
	```sh
	file main.exe
	# main.exe: PE32 executable (console) Intel 80386, for MS Windows
	```

7. Run it! [Wine](https://www.winehq.org/) is your friend.
	```sh
	wine main.exe
	```

	![screenshot of main.exe](http://lbguilherme.com/screenshot/e97fbc3201d9829a500bd8880af6f513.jpg)
