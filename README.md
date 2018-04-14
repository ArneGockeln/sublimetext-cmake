# sublimetext-cmake
This project sets up Sublime Text 3 as C++ IDE with CMake Build System. It is possible to build right from ST3 with shortcut CMD+B. With `cmake` the build system generates the makefile, `make` compiles the binary and cmake copies the binary to the build/ folder.

The repository contains all required files for proper CMake configuration and a basic src/main.cpp file. However I installed a bunch of ST3 plugins to use ST3 as my main C++ IDE. The folder structure is needed, but you can change it within the `projectname.sublime-project` and `CMakeLists.txt` files.

I am using macos High Sierra 10.13.4. 

## Dependencies
I use `clang` as my compiler

```bash
$ clang -v
Apple LLVM version 9.1.0 (clang-902.0.39.1)
Target: x86_64-apple-darwin17.5.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

Of course you need `cmake` in your PATH variable.
```bash
# this is in my ~/.bash_profile
export PATH="$PATH:/Applications/CMake.app/Contents/bin"
```

```bash
$ cmake --version
cmake version 3.11.0
```

## ST3 Plugins
I used the following ST3 plugins to setup ST3 as C++ IDE and make all work.

- CMake https://packagecontrol.io/packages/CMake
- CMakeEditor https://packagecontrol.io/packages/CMakeEditor
- DocBlockr https://packagecontrol.io/packages/DocBlockr
- EasyClangComplete https://packagecontrol.io/packages/EasyClangComplete

## ST3 Build System
The build system is called "cmake" and is defined in the file `projectname.sublime-project`. That means it is only available inside this project. 

```json
{
    "name": "cmake",
    "shell_cmd": "cd ${project_path}/build && cmake .. && make -j4",
    "file_regex": "/([^/:]+):(\\d+):(\\d+): "
}
```

Information about how to extend the build system can be found here https://www.sublimetext.com/docs/3/build_systems.html. Note: the `make -j4` command allows make to use 4 parallel jobs.

## Test
Open the `projectname.sublime-project` file by typing

```bash
$ subl projectname.sublime-project
```

Hit `CMD+B`. The console opens and shows build information:

```
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/arnegockeln/sourcecode/cpp/sublimetext-cmake/build
Scanning dependencies of target projectname
[ 50%] Building CXX object src/CMakeFiles/projectname.dir/main.cpp.o
[100%] Linking CXX executable projectname
[100%] Built target projectname
[Finished in 0.9s]
```

Run binary `projectname` in build/.

```bash
./build/projectname
```
