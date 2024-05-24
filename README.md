# PP_Driver

This project will allow you to remove protection for a given process and put some back through a driver and a client.

Code used and learned through Zero-Point Security course on Offensive Driver Development. You can find a link right [there](https://training.zeropointsecurity.co.uk/courses/offensive-driver-development).

The code structure look like this:

|---- `driver.h` <- header needed both for client and driver source code

|---- `client.cpp` <- client's source code that interacts with the driver

|---- `driver.cpp` <- driver's source code

Thanks to this repo you can build two separate solutions. One of them being the driver himself.

## How to load the driver after building it ?

1. Build `driver.cpp` with `driver.h` included.
2. Then fetch the `.sys` file that comes out of this build in your `debug` folder.
3. Get to your target machine and drop the `.sys` file there.
4. Create a service out of the `.sys` file like so: `sc create MyDriver type= kernel binPath= C:\MyDriver\Driver.sys`
5. Query it to make sure the machine created your service: `sc qc MyDriver`
6. Then start it like that: `sc start MyDriver`

## How to use the client side after dropping / running the driver in a service ?
 
1. Build `client.cpp` with `driver.h` in a separate solution.
2. Drop the `.exe` that comes out of the build into the target
3. Open a terminal and feel free to target any process you'd like to tear the protection down or mimic the protection of `SgrmBroker.exe`

## Few things to note before leaving...

1. Not sure if the code will work at any time given on your side. The latest Windows `SDK`, `MSVC` and `WDK` available to you when seeing this repo might not be compatible with the code provided.
2. Be **EXTRA** cautious when building the project. Before actually building it, you should modify in the `CheckWindowsVersion` function, these two checks:
  - `osInfo.dwMajorVersion` with the Windows version your target is running (10 || 11)
  - `osInfo.dwBuildNumber` with the Windows build number your target is running (in the code provided to you it was `19044`, you can easily enumerate this on your target through the `systeminfo` command for example)
3. Last but not least feel free to tweak this code around, if you any features or safe check you'd like to implement feel free to do so !

