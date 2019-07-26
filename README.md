# Branch of osquery 3.3.2 for Orbital

This branch has changes that has changes used by Cisco for Orbital with the aim of contributing these changes back to the original osquery project. This is branched off of version 3.3.2 and some changes were made to allow building as the original build scripts no longer worked with some locations that files were downloaded from no longer existing, so you will need to follow the instructions below in order to build osquery.

## Building osquery

In order to build osqueryd.exe the following software needs to be installed:

* [Git for Windows](https://git-scm.com/download/win)
* [Build Tools for Visual Studio 2019](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019) - Make sure to select "C++ build tools" in the installer
* [CMake](https://cmake.org/download/) - Select "Add CMake to the system PATH for all users" during installation

You will also want to add `C:\ProgramData\chocolatey\bin` to the `PATH` environment variable for the system as this doesn't exactly get setup properly by the osquery build scripts.

Once the software above has been installed, go to "Start -> Visual Studio 2019 -> x64 Native Tools Command Prompt for VS 2019" in the Start menu and make sure to launch it as an administrator. With the command prompt open, navigate to a folder on the system you want to place your work folders in. Once in that folder, perform a clone of the osquery git repo:
```
git clone git@github.com:threatgrid/osquery.git
```
Change into the folder and checkout the 3.3.2 branch:
```
cd osquery
git checkout v3.3.2
```
Run the development environment setup script. This only needs to be run once and does not need to be used for each time osqueryd.exe is built:
```
tools\make-win64-dev-env.bat
```
When the script is done setting up the environment, setup a folder to perform the build and run cmake to perform the build:
```
mkdir build
cd build
cmake ..
cmake --build . --config RelWithDebInfo -j
```
When the build has successfully finished, you can find a copy of the binary under `build\osquery\RelWithDebInfo\osqueryd.exe` in the git repo folder. Building again with the cmake commands should not require starting a command prompt as an administrator, that is only required for the development environment setup scripts.