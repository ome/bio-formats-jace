# Bio-Formats JACE C++ bindings

[![Build Status](https://travis-ci.org/ome/bio-formats-jace.png)](https://travis-ci.org/ome/bio-formats-jace)

Note that this is a legacy project and is no longer actively maintained. Use
at your own risk.

##Introduction

To make Bio-Formats accessible to software written in C++, we have
created a Bio-Formats C++ interface. It uses
[LOCI's jar2lib program](http://loci.wisc.edu/software/jar2lib) to generate a
C++ proxy class for each equivalent Bio-Formats Java class. The resulting
proxies are then compiled into a library, which represents the actual
interface from C++ to Bio-Formats. Using this library in your projects gives
you access to the image support of Bio-Formats.

The JACE C++ bindings come with some standalone examples which you can use as
a starting point in your own project:

- [showinf](https://github.com/ome/bio-formats-jace/blob/master/src/main/cppwrap/showinf.cpp)
- [minimum_writer](https://github.com/ome/bio-formats-jace/blob/master/src/main/cppwrap/minimum_writer.cpp)

Other projects using the JACE C++ bindings include:

- [WiscScan](http://loci.wisc.edu/software/wiscscan) which uses the JACE C++
  bindings to write [OME-TIFF files](https://www.openmicroscopy.org/site/support/ome-model/ome-tiff/).
- [Video Spot Tracker](http://cismm.cs.unc.edu/resources/software-manuals/video-spot-tracker-manual) which uses the JACE C++ bindings to add Bio-Formats
  support since version 8.10.

##Build instructions

This package provides language bindings for calling into the Bio-Formats Java
library from C++ in a cross-platform manner. As of this writing the bindings
are functional with GCC on Linux and Mac OS X systems, as well as with Visual
C++ 2005 and Visual C++ 2008 on Windows.

**Note that the JACE C++ bindings require Java 7 to build and run. They do
not work with Java 8.**

###Compile-time dependencies

To build the Bio-Formats C++ bindings from source, the following modules are
required:

- [Apache Maven](http://maven.apache.org/)
     Maven is a software project management and comprehension tool. Along with
     Ant, it is one of the supported build systems for the Bio-Formats Java
     library, and is used to generate the Bio-Formats C++ bindings.

- [CMake](http://www.cmake.org/)
     CMake is a cross-platform, open source build system generator, commonly
     used to build C++ projects in a platform-independent manner. CMake
     supports GNU make as well as Microsoft Visual Studio, allowing the
     Bio-Formats C++ bindings to be compiled on Windows, Mac OS X, Linux and
     potentially other platforms.

- [Boost Thread](http://www.boost.org/)
     Boost is a project providing open source portable C++ source libraries.
     It has become a suite of de facto standard libraries for C++. The
     Bio-Formats C++ bindings require the Boost Thread module in order to
     handle C++ threads in a platform independent way.

- [Java Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/)
     Version 6 or 7 is required; version 8 is not currently supported.
     At runtime, only the Java Runtime Environment (JRE) is necessary
     to execute the Bio-Formats code. However, the full J2SE
     development kit is required at compile time on some platforms
     (Windows in particular), since it comes bundled with the |JVM|
     shared library (jvm.lib) necessary to link with Java.

For information on installing these dependencies, refer to the section for
your specific platform below.

###How to build

The process of building the Bio-Formats C++ bindings is divided into two
steps:

1. Generate a C++ project consisting of "proxies" which wrap the Java code.
   This step utilizes the Maven project management tool, specifically a
   Maven plugin called cppwrap.

2. Compile this generated C++ project. This step utilizes the cross-platform
   CMake build system.

For details on executing these build steps, refer to the section for your
specific platform below.

###Build results

If all goes well, the build system will:

1. Generate the Bio-Formats C++ proxy classes
2. Build the Jace C++ library
3. Build the Java Tools C++ library
4. Build the Bio-Formats C++ shared library
5. Build the showinf and minimum_writer command line tools for testing the
   functionality.

Please be patient, as the build may require several minutes to complete.

Afterwards, the dist/formats-bsd subdirectory will contain the following
files:

1. libjace.so / libjace.jnilib / jace.dll :
     Jace shared library

2. libformats-bsd.so / libformats-bsd.dylib / formats-bsd.dll :
     C++ shared library for BSD-licensed readers and writers

3. jace-runtime.jar :
     Jace Java classes needed at runtime

4. bioformats_package.jar :
     Bio-Formats Java library needed at runtime
-
5. libjtools.so / libjtools.jnilib / jtools.dll :
     Java Tools shared library

6. showinf / showinf.exe :
     Example command line application

7. minimum_writer / minimum_writer.exe :
     Example command line application

Items 1-4 are necessary and required to deploy Bio-Formats with your C++
application. Item 5 (jtools) is a useful helper library for managing the Java
virtual machine from C++, but is not strictly necessary to use Bio-Formats.
All other files, including the example programs and various build files
generated by CMake, are not needed.

If you prefer, instead of using the bioformats_package.jar bundle, you can
provide individual JAR files as appropriate for your application. For details,
see [using Bio-Formats as a Java library](https://www.openmicroscopy.org/site/support/bio-formats/developers/java-library.html).

