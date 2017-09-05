#!python 
import platform
import os
import sys
import glob

print("Project Script Config!")
#print("Current Dir: " + os.getcwd())

#get the mode flag from the command line
#default to 'release' if the user didn't specify
#projectmode = ARGUMENTS.get('mode', 'release')   #holds current mode
projectmode = ARGUMENTS.get('mode', 'debug')   #holds current mode
#print("MODE: "+projectmode)

projecttool = ARGUMENTS.get('tool', 'mingw')   #holds current mode
#projecttool = 'window'

print("**** TOOL:" + projecttool)

#check if the user has been naughty: only 'debug' or 'release' allowed
if not (projectmode in ['debug','release']):
	print("Error: expected 'debug' or 'release', found: " + projectmode)

#tell the user what we're doing
print('**** Compiling in ' + projectmode + ' mode...')

#-------

project = 'main'					#holds the project name
buildroot = './bin/' + projectmode		#holds the root of the build directory tree
builddir = './' + project  				#holds the build directory for this project
targetpath = buildroot + '/' + project	#holds the path to the executable in the build directory

if projecttool == 'mingw': #mingw tool
	env = Environment(ENV = os.environ, tools = ['mingw'])
	env.Append(CCFLAGS = '-g')#-g (debug) flag
	#link lib
	env.Append(LINKFLAGS='-static-libgcc -static-libstdc++')
elif projecttool == 'window': #window tool default to vs2017
	#http://scons.org/doc/0.97/HTML/scons-man.html
	#need to lanuch vcvars32.bat script so it can be add to os.environ else it will display 'cl' is not recognized as an internal or external command
	#this will deal with the Visual Studio 
	env = Environment(ENV = os.environ) #this load user complete external environment
else:
	#default current tool from os
	env = Environment(ENV = os.environ) #this load user complete external environment
	#pass

system = platform.system()

thirdparty_libs = []

if system=='Windows':
	print("**** OS: WINDOW")
	# Something to do with link error
	env.Append(LINKFLAGS=['/SUBSYSTEM:CONSOLE'])
	#inlcude file
	env.Append(CPPPATH=['C:\\SDL2-2.0.5\\include','imgui'])
	#Repository('C:\\SDL2-2.0.5\\include','imgui')
	#build lib file
	env.Library('bin\\imgui',Glob('imgui\\*.cpp'))

	#env.Library(target='imgui_impl_sdl',LIBS=['SDL2','SDL2main','SDL2test'],LIBPATH=['C:\\SDL2-2.0.5\\lib\\x86'])
	#env.Library('imgui_impl_sdl',LIBS=['SDL2','SDL2main','SDL2test'],LIBPATH=['C:\\SDL2-2.0.5\\lib\\x86'])
	#env.Append(LIBS=File('C:\\SDL2-2.0.5\\lib\\x86\\SDL2.dll'))
	#env.Append(LIBS=['opengl32','SDL2main','SDL2','SDL2test'],LIBPATH=['C:\\SDL2-2.0.5\\lib\\x86'],RPATH=[os.path.abspath(os.curdir + "/bin")])
	dir = os.getcwd()
	print(dir)
	thirdparty_libs += env.Glob( dir +'/libs/*.dll')

	#for lib in thirdparty_libs:
		#name_parts = os.path.splitext(lib.name)
		#print(lib.name)
		#if name_parts[1] == '.dll':
			#print("found!")
			# TODO: Need to publish 'libfoo.dylib' or 'libfoo.a' as both
			# 'libfoo' and 'foo'.  Need to clean up sconscripts to remove 'lib' prefix
			# from all libs for mac, linux.
			#lib_basename = name_parts[0]
			#print(lib_basename)
			#env.Publish(lib_basename, 'run', lib)
			#env.Publish(lib_basename[3:], 'run', lib)
			
	#copy file or folder to bin dir
	env.Install("bin","libs\SDL2.dll")

	#application
	env.Program('bin\\main',Glob('main\\*.cpp'),LIBS=['opengl32','imgui','SDL2main','SDL2','SDL2test'],LIBPATH=['.','bin','C:\\SDL2-2.0.5\\lib\\x86'])
	#env.Program('bin\\main',Glob('main\\*.cpp'),LIBS=['opengl32','imgui','SDL2main','SDL2','SDL2test'],LIBPATH=['.','bin','C:\\SDL2-2.0.5\\lib\\x86'])
	

print("**** Script Finish Here!")