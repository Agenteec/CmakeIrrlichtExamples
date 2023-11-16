# CMakeList.txt: проект CMake для IrrlichtExamples; включите исходный код и определения,
# укажите здесь логику для конкретного проекта.
#
cmake_minimum_required (VERSION 3.8)

# Включение горячей перезагрузки для компиляторов MSVC, если поддерживается.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()


if(WIN32)
    execute_process(COMMAND cmd /c echo %USERPROFILE% OUTPUT_VARIABLE USER_PROFILE)
    string(STRIP "${USER_PROFILE}" USER_PROFILE)
else()
    message(FATAL_ERROR "This script is designed for Windows only.")
endif()
include("${USER_PROFILE}/vcpkg/scripts/buildsystems/vcpkg.cmake")
set(VCPKG_PATH "${USER_PROFILE}/vcpkg")
set(VCPKG_INCLUDE_DIR "${VCPKG_PATH}/installed/${VCPKG_TARGET_TRIPLET}/include")
set(VCPKG_LIBRARY_DIR "${VCPKG_PATH}/installed/${VCPKG_TARGET_TRIPLET}/lib")
set(VCPKG_BINARY_DIR "${VCPKG_PATH}/installed/${VCPKG_TARGET_TRIPLET}/bin")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/CMakeModules")

# Find the Irrlicht library
find_library(
    Irrlicht_LIB
    NAMES Irrlicht
    PATHS ${VCPKG_LIBRARY_DIR}/irrlicht/lib/directory
)

# Include the Irrlicht header files
find_path(
    Irrlicht_INCLUDE_DIR
    NAMES irrlicht.h
    PATHS "${VCPKG_INCLUDE_DIR}/irrlicht"
)


include_directories(${VCPKG_INCLUDE_DIR} ${Irrlicht_INCLUDE_DIR})


find_package(irrlicht CONFIG REQUIRED)
project ("IrrlichtExamples")

# Добавьте источник в исполняемый файл этого проекта.
add_executable (HelloWorld "01.HelloWorld/main.cpp")
add_executable (Quake3Map "02.Quake3Map/main.cpp")
add_executable (CustomSceneNode "03.CustomSceneNode/main.cpp")
add_executable (Movement "04.Movement/main.cpp")
add_executable (UserInterface "05.UserInterface/main.cpp")
add_executable (2DGraphics "06.2DGraphics/main.cpp")
add_executable (Collision "07.Collision/main.cpp")
add_executable (SpecialFX "08.SpecialFX/main.cpp")
add_executable (Meshviewer "09.Meshviewer/main.cpp")
add_executable (Shaders "10.Shaders/main.cpp")

add_executable (PerPixelLighting "11.PerPixelLighting/main.cpp")
add_executable (TerrainRendering "12.TerrainRendering/main.cpp")
add_executable (RenderToTexture "13.RenderToTexture/main.cpp")
add_executable (Win32Window "14.Win32Window/main.cpp")
add_executable (LoadIrrFile "15.LoadIrrFile/main.cpp")
add_executable (Quake3MapShader "16.Quake3MapShader/main.cpp")
add_executable (HelloWorld_Mobile "17.HelloWorld_Mobile/main.cpp")
add_executable (SplitScreen "18.SplitScreen/main.cpp")
add_executable (MouseAndJoystick "19.MouseAndJoystick/main.cpp")
add_executable (ManagedLights "20.ManagedLights/main.cpp")
add_executable (Quake3Explorer "21.Quake3Explorer/main.cpp" "21.Quake3Explorer/q3factory.cpp" "21.Quake3Explorer/q3factory.h" "21.Quake3Explorer/sound.cpp" "21.Quake3Explorer/sound.h")
add_executable (MaterialViewer "22.MaterialViewer/main.cpp")
add_executable (SMeshHandling "23.SMeshHandling/main.cpp")
add_executable (CursorControl "24.CursorControl/main.cpp")
add_executable (XmlHandling "25.XmlHandling/main.cpp")
add_executable (OcclusionQuery "26.OcclusionQuery/main.cpp")


target_link_libraries(HelloWorld ${Irrlicht_LIB})
target_link_libraries(Quake3Map ${Irrlicht_LIB})
target_link_libraries(CustomSceneNode ${Irrlicht_LIB})
target_link_libraries(Movement ${Irrlicht_LIB})
target_link_libraries(UserInterface ${Irrlicht_LIB})
target_link_libraries(2DGraphics ${Irrlicht_LIB})
target_link_libraries(Collision ${Irrlicht_LIB})
target_link_libraries(SpecialFX ${Irrlicht_LIB})
target_link_libraries(Meshviewer ${Irrlicht_LIB})
target_link_libraries(Shaders ${Irrlicht_LIB})

target_link_libraries(PerPixelLighting ${Irrlicht_LIB})
target_link_libraries(TerrainRendering ${Irrlicht_LIB})
target_link_libraries(RenderToTexture ${Irrlicht_LIB})
target_link_libraries(LoadIrrFile ${Irrlicht_LIB})
target_link_libraries(Quake3MapShader ${Irrlicht_LIB})
target_link_libraries(HelloWorld_Mobile ${Irrlicht_LIB})
target_link_libraries(Win32Window ${Irrlicht_LIB})
target_link_libraries(SplitScreen ${Irrlicht_LIB})
target_link_libraries(MouseAndJoystick ${Irrlicht_LIB})
target_link_libraries(ManagedLights ${Irrlicht_LIB})
target_link_libraries(Quake3Explorer ${Irrlicht_LIB})
target_link_libraries(MaterialViewer ${Irrlicht_LIB})
target_link_libraries(CursorControl ${Irrlicht_LIB})
target_link_libraries(XmlHandling ${Irrlicht_LIB})
target_link_libraries(OcclusionQuery ${Irrlicht_LIB})


if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET HelloWorld PROPERTY CXX_STANDARD 20)
  set_property(TARGET Quake3Map PROPERTY CXX_STANDARD 20)
  set_property(TARGET CustomSceneNode PROPERTY CXX_STANDARD 20)
  set_property(TARGET Movement PROPERTY CXX_STANDARD 20)
  set_property(TARGET UserInterface PROPERTY CXX_STANDARD 20)
  set_property(TARGET 2DGraphics PROPERTY CXX_STANDARD 20)
  set_property(TARGET Collision PROPERTY CXX_STANDARD 20)
  set_property(TARGET SpecialFX PROPERTY CXX_STANDARD 20)
  set_property(TARGET Meshviewer PROPERTY CXX_STANDARD 20)
  set_property(TARGET Shaders PROPERTY CXX_STANDARD 20)
  set_property(TARGET PerPixelLighting PROPERTY CXX_STANDARD 20)
  set_property(TARGET TerrainRendering PROPERTY CXX_STANDARD 20)
  set_property(TARGET RenderToTexture PROPERTY CXX_STANDARD 20)
  set_property(TARGET LoadIrrFile PROPERTY CXX_STANDARD 20)
  set_property(TARGET Quake3MapShader PROPERTY CXX_STANDARD 20)
  set_property(TARGET HelloWorld_Mobile PROPERTY CXX_STANDARD 20)
  set_property(TARGET Win32Window PROPERTY CXX_STANDARD 20)
  set_property(TARGET SplitScreen PROPERTY CXX_STANDARD 20)
  set_property(TARGET MouseAndJoystick PROPERTY CXX_STANDARD 20)
  set_property(TARGET ManagedLights PROPERTY CXX_STANDARD 20)
  set_property(TARGET Quake3Explorer PROPERTY CXX_STANDARD 20)
  set_property(TARGET MaterialViewer PROPERTY CXX_STANDARD 20)
  set_property(TARGET CursorControl PROPERTY CXX_STANDARD 20)
  set_property(TARGET XmlHandling PROPERTY CXX_STANDARD 20)
  set_property(TARGET OcclusionQuery PROPERTY CXX_STANDARD 20)
endif()


# TODO: Добавьте тесты и целевые объекты, если это необходимо.
