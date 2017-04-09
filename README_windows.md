Build requirements:
- vs2015
- clang (I'm using LLVM-5.0.0-r295586-win64)
- cmake (>= 3.7)
- nvml (1.2+wtp1, newer versions won't work)

Workaround CMake bug:
- Open C:\Program Files\CMake\share\cmake-${version}\Modules\Platform\Windows-MSVC.cmake
- Replace all CMAKE_VS_PLATFORM_TOOLSET with XXX_CMAKE_VS_PLATFORM_TOOLSET
- Save

Build:
- mkdir build
- cd build
- cmake .. -DPMEMOBJ_PATH=%PMEMOBJ_PATH%/nvml-debug/ -DCMAKE_MODULE_PATH=%PMEMFILE_PATH%/src/libpmemfile-posix/ -DBUILD_LIBPMEMFILE=0 -DCMAKE_BUILD_TYPE=Debug -DCMAKE_GENERATOR_PLATFORM=x64 -G"Visual Studio 14 2015" -T"LLVM-vs2014" -DDEVELOPER_MODE=0
- msbuild pmemfile.sln
- ctest -C Debug
