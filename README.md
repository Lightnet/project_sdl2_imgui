# project_sdl2_imgui

Project Name: project_sdl2_imgui

Created by: Lightnet

License: MIT

Programs:
 * Visual Studio Code
 * Python 2.7.x
  * Scons (script builds)
 * VS2017 Window 10 (compiler tool)
 * SDL 2.0.5 (www.libsdl.org)
 * imgui v1.51 (https://github.com/ocornut/imgui)

Information: Simple compile build using vs2017 tool to display sdl2 with imgui test.

Note: It is set to debug since I have not yet work on release compile yet.

The dll is the current build from libs folder testing.

Configs:
 * ./SConstrct 
 * ./.vscode/Settings.json

[Scons Builds]:

[Mingw]

   `scons tool=mingw`

   GL3 does not work for some reason. Just an error for "wglGetProcAddress"

[window 10 | viusal studio]

   `scons tool=window`

Credits: 
 * http://www.damianperdiz.com/scons-cross-platform-build-sdl2-and-imgui-example.html