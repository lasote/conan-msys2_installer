## This repository holds a conan recipe for MSYS2.

[![Build status](https://ci.appveyor.com/api/projects/status/m57753vg4rbyy53h/branch/stable/20161025?svg=true)](https://ci.appveyor.com/project/BinCrafters/conan-msys2-installer/branch/stable/20161025)

[Conan.io](https://conan.io) package for [MSYS](http://www.msys2.org) project

The packages generated with this **conanfile** can be found in [Bintray](https://bintray.com/bincrafters/public-conan/msys2_installer%3Abincrafters).

MSYS2 is software distribution and a building platform for Windows. It provides a Unix-like environment, a command-line interface and a software repository making it easier to install, use, build and port software on Windows.  Many C++ projects are setup to be built with MSYS2 when built on Windows, rather than MSBuild. 

## Intended Use

This package is intended to be used in Conan recipes as a `build_requires`.  

[Conan `build_requires` feature Explained](http://conanio.readthedocs.io/en/latest/reference/conanfile/attributes.html#build-requires)

## Conan "latest" version convention

MSYS2 never adopted semantic versioning, so this package offers a unique versioning option on the packages by using a "conan alias" named "latest". 

[Conan Alias feature Explained](http://conanio.readthedocs.io/en/latest/reference/commands/alias.html?highlight=conan%20alias)

In summary, users can reference the version of "latest" in their requirements as shown in the example below to get the latest release of MSYS2.  "latest" is just an alias which redirects to an actual version of an MSYS2 package. MSYS2 rarely releases new versions, but when they do Bincrafters will compile, create and upload binaries for the package and "latest" will be updated to point to the new version.  Because MSYS2 does not use semantic versioning, a datestamp will be used as the version number on the concrete Bincrafters packages for MSYS2 and the `source()` method of each version of the recipe will use the latest tarball from the msys2.org repository here:  http://repo.msys2.org/distrib. 

## For Users: Use this packages

### Basic setup

    $ conan install msys2_installer/latest@bincrafters/stable

### Project setup

If you handle multiple dependencies in your project is better to add a *conanfile.txt*

    [requires]
    msys2_installer/latest@bincrafters/stable

    [generators]
    txt

Complete the installation of requirements for your project running:

    $ mkdir build && cd build && conan install ..
	
Note: It is recommended that you run conan install from a build directory and not the root of the project directory.  This is because conan generates *conanbuildinfo* files specific to a single build configuration which by default comes from an autodetected default profile located in ~/.conan/profiles/default .  If you pass different build configuration options to conan install, it will generate different *conanbuildinfo* files.  Thus, they should not be added to the root of the project, nor committed to git. 

## For Packagers: Publish this Package

The example below shows the commands used to publish to bincrafters conan repository. To publish to your own conan respository (for example, after forking this git repository), you will need to change the commands below accordingly. 

## Build and package 

The following command both runs all the steps of the conan file, and publishes the package to the local system cache.  

    $ conan create bincrafters/stable
	
## Add Remote

	$ conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"

## Upload
	
To upload a package with an alias involved, it's a three-step process. 

The first step is standard, upload the concrete package you've recently built:

    $ conan upload msys2_installer/20161025@bincrafters/stable --all -r bincrafters

The second step is to create or update the "alias package" on your local machine: 

	$ conan alias msys2_installer/latest@bincrafters/stable msys2_installer/20161025@bincrafters/stable

The third step is to upload the alias package:

	$conan upload msys2_installer/latest@bincrafters/stable --all -r bincrafters
	

