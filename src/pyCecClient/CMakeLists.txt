project(pyCecClient)
cmake_minimum_required(VERSION 3.12.0)

# Python
if(WIN32 AND "${MSVC_C_ARCHITECTURE_ID}" STREQUAL "X86")
  set(PYTHON_USE_VERSION 2)
endif()

if(PYTHON_USE_VERSION EQUAL 2)
  include(FindPython2)
  find_package(Python2)
  set(PYTHONLIBS_FOUND "${Python2_FOUND}")
else()
  set(PYTHON_LIBRARIES "C:/../../AppData/Local/Programs/Python/Python38/libs")
  set(PYTHON_INCLUDE_PATH "C:/../../AppData/Local/Programs/Python/Python38/include")

  include(FindPythonLibs)
  find_package(PythonLibs)

  if(0)
    message(STATUS "PlatformSupport PYTHON_LIBRARY: ${PYTHON_LIBRARY}")
    message(STATUS "PlatformSupport PYTHON_INCLUDE_DIR: ${PYTHON_INCLUDE_DIR}")
    message(STATUS "PlatformSupport PYTHONLIBS_FOUND: ${PYTHONLIBS_FOUND}")
    message(STATUS "PlatformSupport PYTHON_LIBRARIES: ${PYTHON_LIBRARIES}")
    message(STATUS "PlatformSupport PYTHON_INCLUDE_DIRS: ${PYTHON_INCLUDE_DIRS}")
    message(STATUS "PlatformSupport PYTHONLIBS_VERSION_STRING: ${PYTHONLIBS_VERSION_STRING}")
  endif()
endif()

if(PYTHONLIBS_FOUND)
  if (WIN32)
    install(PROGRAMS pyCecClient.py
            DESTINATION python/.)
  else()
    install(PROGRAMS pyCecClient.py
            DESTINATION bin/.
            RENAME pyCecClient)
  endif()
endif()
