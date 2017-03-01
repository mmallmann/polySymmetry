## ----------------------------------------------------------------------
'''
SConscript for polySymmetry plugin set
'''
## ----------------------------------------------------------------------

import os, sys
platform = sys.platform

INSTALL_DIRECTORY = "./polySymmetry/plug-ins"
PLUGIN_NAME = 'polySymmetry'

env = Environment(
	CPPDEFINES=[
		# '_DEBUG',
		'_BOOL',
		'REQUIRE_IOSTREAM',
		'MAYA_PARALLEL'
	],

	LIBS = [
		'OpenMaya',
		'OpenMayaAnim',
		'OpenMayaUI',
		'Foundation',
	],
)

ARCHFLAGS = ['-m64', '-mavx', '-fPIC']
CFLAGS = [
	'-O3',
	'-mmacosx-version-min=10.11'
	] + ARCHFLAGS

CCFLAGS = CFLAGS + [
	'-fno-gnu-keywords', '-fpascal-strings',
	'-std=c++14', '-Wc++11-extensions', '-Wc++11-long-long',
	"-stdlib=libc++",
	]

LFLAGS = CCFLAGS + [
	'-headerpad_max_install_names', '-framework', 'System',
	'-framework', 'SystemConfiguration', '-framework', 'CoreServices',
	'-framework', 'Cocoa', '-framework', 'ApplicationServices',
	'-framework', 'IOKit',
	'-Wl,-exported_symbol,__Z16initializePlugin7MObject',
	'-Wl,-exported_symbol,__Z18uninitializePlugin7MObject'
	]

MAYA_BASE = "/Applications/Autodesk/maya2017"
MAYA_HEADERS_DIR = MAYA_BASE + "/include"
MAYA_LIBRARY_DIR = MAYA_BASE + "/Maya.app/Contents/MacOS"
env.Append( CFLAGS=CFLAGS )
env.Append( CCFLAGS=CCFLAGS )
env.Append( LINKFLAGS=LFLAGS )
env.Append( CPPDEFINES=[
			'MAC_PLUGIN', 'OSMac_', 'CC_GNU_',
			'OSMacOSX_', 'REQUIRE_IOSTREAM', 'OSMac_MachO_',
			'_LANGUAGE_C_PLUS_PLUS'
			] )

env.Replace( CC="clang" )
env.Replace( CXX="clang++" )
TARGET = PLUGIN_NAME + '.bundle'

env.Append( CPPPATH=[ MAYA_HEADERS_DIR, 'pystring' ] )
env.Append( LIBPATH=[ MAYA_LIBRARY_DIR ] )

sources = (
	Glob('src/*.cpp') +
	Glob('pystring/*.cpp')
)

env.SharedLibrary( target=TARGET, source=sources, SHLIBPREFIX='' )

## set the install directory yourself
env.Install( INSTALL_DIRECTORY, TARGET )
env.Alias( 'install', INSTALL_DIRECTORY )


