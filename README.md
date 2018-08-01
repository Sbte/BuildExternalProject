# BuildExternalProject
Build a CMake ExternalProject during configure time. This allows for inclusion of an ExternalProject using `find_package`. The module can be downloaded dynamically by using

```
file(DOWNLOAD
  https://raw.githubusercontent.com/Sbte/BuildExternalProject/master/BuildExternalProject.cmake
  ${CMAKE_BINARY_DIR}/external/cmake/BuildExternalProject.cmake TIMEOUT 5)

set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_BINARY_DIR}/external/cmake" PARENT_SCOPE)
```

and then an external project, for instance Google Test can be included

```
include(BuildExternalProject)
BuildExternalProject(
  GTest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG release-1.8.0)

BuildExternalProject_find_package(GTest)
```

The `BuildExternalProject` function accepts the same options as `ExternalProject_Add`. After this, `BuildExternalProject_find_package` can be used to find the package. Any variables set by the external project can be used as one would do after using `find_package` for any other package.
