My STM32CubeIDE installation was running OK on Ubuntu 23 but then it broke; I think it was when I installed the separate STM32Cube Programmer. I found libncurses.so.5 in /snap/core18/2812/lib/x86_64-linux-gnu so I did

sudo vi /etc/ld.so.conf and added the line

/snap/core18/2812/lib/x86_64-linux-gnu

Remember to sudo ldconfig at the end